<div align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&pause=1000&color=F75C7E&center=true&vCenter=true&width=500&lines=Hi%2C+I'm+Shivam+%F0%9F%91%8B;Computer+Science+%40+NIT+Durgapur;Backend+%26+Systems+Engineer;JPMC+Code+For+Good+2025" alt="Typing SVG" />
</div>

<p align="center">
  <em>Computer Science student at NIT Durgapur passionate about scalable systems, backend architecture, and performance optimization.</em>
</p>

---

## About Me

- 🎓 Final-year **CS Engineering** at **NIT Durgapur** · **9.71 CGPA**
- 🧠 I learn by building from scratch — BitTorrent clients, web crawlers, chat systems
- 🔬 I treat every project like a systems paper: define the bottleneck, architect around it, then benchmark until the numbers prove it
- 🛠️ Currently deep in **Go** — building protocol-level and infrastructure projects to sharpen my systems thinking
- 🏅 **JPMC Code For Good 2025** selectee 
- 📫 **gangulyshivam6@gmail.com**

---

## Featured Systems

### 🔗 High-Performance URL Shortener &nbsp; [![GitHub](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/MonarchRyuzaki/URL-Shortener)

**Problem**
- URL shortening services at scale face bottlenecks in redirect latency, database write throughput, and cache invalidation under concurrent load

**Solution**
- Multi-tier architecture with **Redis caching**, **NGINX reverse proxy**, and **containerized Node.js workers** behind a load balancer
- Write-behind caching and connection pooling to minimize database round-trips

**Outcome**
- **700+ req/s** sustained throughput · **sub-500ms p99 latency**
- Horizontally scalable via Docker Compose
- Benchmarked with `wrk` under sustained concurrent connections

<p align="center">
  <img src="./docs/url-shortener.png" alt="URL Shortener Architecture" width="75%" />
</p>

### 💬 Real-Time Chat System &nbsp; [![GitHub](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/MonarchRyuzaki/Real-Time-Chat-App)

**Problem**
- Scalability bottlenecks in monolithic WebSocket servers
- High-volume write saturation on relational databases
- Message loss during cross-server delivery in clustered environments

**Solution**
- Decoupled multi-service architecture (HTTP, Chat WS, Presence WS) behind **NGINX** to isolate concerns and scale independently
- Multi-database strategy: **PostgreSQL** for relational metadata, **Apache Cassandra** for append-heavy message logs
- **Redis Streams** for "at-least-once" message delivery and a centralized **Redis directory** for cross-server routing

**Outcome**
- **721+ msg/s** sustained throughput · **4.3ms mean handshake latency**
- **99.5% success rate** under enterprise stress tests (8,400+ total vusers)
- **5x throughput improvement** over baseline via multi-layered caching (Bloom filters + Redis) and connection pool optimization

<p align="center">
  <img src="./docs/chat-app.png" alt="Chat System Architecture" width="75%" />
</p>

### 🚀 Go BitTorrent Client &nbsp; [![GitHub](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/MonarchRyuzaki/go-bittorrent-client)

**Problem**
- Traditional HTTP downloads are fragile — a dropped connection means lost progress
- Concurrent peer coordination, binary protocol parsing, and shared state management across goroutines
- Graceful handling of unreliable network peers (timeouts, chokes, disconnects)

**Solution**
- Full **BitTorrent v1.0 protocol** in **Go** — handshake, bitfield exchange, pipelining, and SHA-1 piece verification
- **Central Dispatcher ("Manager") pattern** with bitfield-aware piece assignment and fire-and-forget goroutine model
- Per-peer mutexes for maximum download parallelism
- Defensive state management: dead peers permanently banned, connection deadlines reset post-handshake, nil-safe cleanup

**Outcome**
- Fully functional concurrent distributed file transfer over **TCP**
- Parallel piece downloads across the entire peer swarm with **per-peer locking** (zero cross-peer contention)
- Robust error recovery — survived flaky peers, broken pipes, and silent timeouts without crashes

### 🕷️ Concurrent Web Crawler &nbsp; [![GitHub](https://img.shields.io/badge/View_Repo-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/MonarchRyuzaki/Web-Crawler)

**Problem**

- Duplicate fetches waste crawl budget — page X → A and page Y → A both enqueue A without deduplication
- Spider traps (infinite generated pages like `/events/2026/02/`, `/2026/03/`…) consume the entire crawl run on junk
- DNS lookup overhead compounds across thousands of requests to the same domains
- Politeness violations (hammering a single host) trigger IP bans and honeypot detection
- Coordinating URL prioritization, per-host rate limiting, and content deduplication across concurrent workers

**Solution**

- Two-stage frontier: 5 priority queues ranked by OpenPageRank scores (weighted random with exponential decay) → 5 back queues with domain-affinity routing for per-host politeness
- Two-tier URL deduplication: Redis Bloom Filter as a fast "definitely not seen" gate (~1ms), DynamoDB as ground truth for false positives — eliminates ~90% of DB reads
- DynamoDB conditional writes (`attribute_not_exists`) for atomic content storage without read-before-write overhead
- robots.txt compliance with cached Disallow path matching to avoid spider traps and honeypots
- DNS caching via dnscache, SHA-256 content hashing, and go-readability parsing to strip boilerplate before storage
- 5 fetcher workers + 5 processing workers with channel-based coordination

**Outcome**

- ~4 fresh pages/second on a single instance (full pipeline: DNS → robots.txt → fetch → extract → hash → Bloom filter → DynamoDB write)
- Interface-driven architecture (`Frontier`, `Fetcher`, `Parser`, `Storage`, `Metrics`) — swapped from in-memory maps to DynamoDB + Redis with zero changes to the crawl loop
- Correctly avoids spider traps, honeypots, and duplicate work across the entire crawl

<p align="center">
  <img src="./docs/web-crawler.png" alt="Web Crawler Architecture" width="75%" />
</p>

---

## 💼 Experience

### Research Assistant · NIT Durgapur CS Department
**August 2024 – October 2024**

- Developed an EEG signal analysis pipeline processing **15+ datasets**, achieving a **30% improvement in algorithmic efficiency** through optimized computation of Alpha-Beta and Theta-Beta ratios
- **Automated the analysis reporting workflow**, reducing manual processing effort by **60%** and enabling reproducible batch analysis across datasets
- Collaborated with **2 PhD scholars** to refine signal processing algorithms, improving data accuracy by **20%**
- Reduced per-dataset processing time by **40%** through GUI and pipeline optimizations

---

### 🖥️ Core Systems & Languages
<p align="left">
  <img src="https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white" alt="Go" />
  <img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++" />
  <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white" alt="Java" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Lua-2C2D72?style=for-the-badge&logo=lua&logoColor=white" alt="Lua" /> </p>

### 🏗️ Infrastructure & Performance
<p align="left">
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/NGINX-009639?style=for-the-badge&logo=nginx&logoColor=white" alt="NGINX" />
  <img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/Cassandra-1287B1?style=for-the-badge&logo=apache-cassandra&logoColor=white" alt="Cassandra" />
  <img src="https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL" />
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux" />
  <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white" alt="GitHub Actions" />
</p>


<details>
<summary><b>🎨 Frontend & Other Tools (Click to expand)</b></summary>
<br>
<p align="left">
  <img src="https://img.shields.io/badge/React.js-61DAFB?style=flat&logo=react&logoColor=black" />
  <img src="https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs&logoColor=white" />
  <img src="https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white" />
  <img src="https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white" />
</p>
</details>

---

## 🏆 Achievements

| Achievement | Detail |
|---|---|
| 🏅 **JPMC Code For Good 2025** | Selected participant — scalable tech solutions for NGOs |
| 🎯 **JEE Mains 2022** | AIR 7.9K / 1M+ candidates |
| 📈 **Academic** | 9.71 CGPA at NIT Durgapur |

---

<div align="center">

[![Email](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:gangulyshivam6@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shivam-ganguly-357b90255/)
[![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://x.com/Shiryu021)

</div>

---

<div align="center">
  <strong>"Design for scale. Build for clarity. Measure everything."</strong>
</div>
