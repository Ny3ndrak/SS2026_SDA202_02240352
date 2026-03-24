# URL Shortener Design Analysis

## 1. Problem Statement Analysis

### Core Challenge and Scope
The goal is to design a URL shortening service similar to TinyURL. The main challenge is building a system that remains fast, reliable, and scalable under very large traffic volumes while producing short and unique URLs.

### Key Requirements
- **Scale:** The system must handle **100 million new URLs per day**.
- **Write Throughput:** Approximately **1,160 write requests per second**.
- **Read Throughput:** Approximately **11,600 read requests per second**.
- **Storage:** Over **10 years**, the service must support **365 billion records**, requiring about **365 TB of storage**.
- **URL Constraints:** Short URLs should be as compact as possible using the character set `[0-9, a-z, A-Z]`.
- **Availability:** The system must be **highly available** and **fault-tolerant**.
- **Data Assumption:** URLs are treated as **permanent**, with **no updates or deletes**.

## 2. Analysis of the Proposed Solution

### API Design
The service is based on a simple REST-style API:

- `POST` creates a shortened URL.
- `GET` resolves the shortened URL and redirects the user to the original long URL.

This keeps the system easy to understand and aligns well with the two main user actions: shortening and redirecting.

### Redirection Strategy
The author compares two redirect options:

- **301 Permanent Redirect:** Better for reducing server load because browsers can cache the redirect result.
- **302 Temporary Redirect:** Better when the service wants to track analytics such as click counts and traffic sources.

This is a strong design discussion because it shows that redirect choice is not just technical, but also product-driven.

### Storage and Performance Design
The solution starts from a basic hash table idea, then improves it by using:

- A **relational database** for durable storage.
- A **cache** for storing `<shortURL, longURL>` mappings.

Because the system is heavily read-dominant, the cache is essential for reducing database pressure and improving latency.

### URL Shortening Methods
The author evaluates two main strategies:

#### 1. Hashing with Collision Resolution
- Uses hash functions such as **MD5** or **CRC32**.
- Takes the first **7 characters** of the hash.
- If collisions occur, it resolves them by appending extra strings and re-hashing.

This approach works, but it adds collision-handling complexity.

#### 2. Base62 Conversion from Unique IDs
- Converts a unique numeric ID into a **Base62** string.
- Uses characters `[0-9, a-z, A-Z]`.
- Avoids collisions because each numeric ID is already unique.

This is the preferred approach because it is simpler, deterministic, and more scalable.

## 3. Review of the Analysis

### Understanding
The most important takeaway is that **Base62 conversion** is the stronger design choice. Instead of depending on random hashing and collision handling, it converts a guaranteed unique numeric ID into a compact short string.

Another strong point is the justification for a **7-character short code**. Since:

$$
62^7 \approx 3.5 \text{ trillion}
$$

the available key space is large enough to support the target of **365 billion URLs** over 10 years.

### Confusions and Gaps
One important concern is **predictability**. If numeric IDs increase sequentially, then short URLs become easy to guess. That creates both privacy and security issues because users may enumerate nearby links.

The author references distributed unique ID generation, but the current material does not fully explain how IDs are generated in a way that is both:

- **Globally unique**
- **Hard to predict**

This is a meaningful design gap because the entire Base62 method depends on the quality of the ID generator.

### Topics for Further Study
- **Bloom Filters:** Useful for quickly checking whether a short URL may already exist before performing a more expensive database lookup.
- **Rate Limiting:** Needed to prevent abuse, spam, and automated attacks against the shortening API.
- **Database Sharding:** Necessary to distribute hundreds of terabytes of data across multiple machines while maintaining performance.

## 4. Brief Critical Summary

The author's design is a strong blueprint for a production-grade distributed URL shortening service. The decision to prefer **Base62 conversion** over direct hashing is the best part of the solution because it removes most collision-management complexity and gives predictable short URL generation.

The addition of:

- a **cache** for fast reads, and
- a **load balancer** for distributing traffic

helps the system handle the heavy read-to-write ratio efficiently.

At the same time, the design depends heavily on a reliable **distributed unique ID generator**, which becomes a critical system component. It also needs stronger protection layers, especially **rate limiting**, to defend against abuse, scraping, and automated request floods.

## Final Assessment

Overall, this is a solid and scalable design. It demonstrates good system design fundamentals, clear trade-off analysis, and a practical architecture for a real-world URL shortening service. The main areas that need deeper treatment are distributed ID generation, security hardening, and large-scale data partitioning.
