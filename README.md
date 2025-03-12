CleanStart Redis Image 
📌 Introduction
The cleanstart/redis image provides a high-performance, in-memory, and production-ready data structure store that can be used as a database, cache, and message broker.

✔️ In-memory performance
✔️ Versatile data structures
✔️ Container optimized

It supports various use cases, including caching, real-time analytics, pub/sub messaging, and session storage.

📌 Why Use?
✔️ Lightning Fast → Sub-millisecond response times with in-memory operations.
🚀 Scalable → Support for clustering and replication for high availability.
🛠️ Feature Rich → Extensive command set for various data structures (strings, lists, sets, hashes).
📦 Lightweight → Minimal resource footprint optimized for containerized environments.

---

⬇️ Download This Image

This image is available on Docker Hub:
cleanstart/redis on Docker Hub

```
docker pull cleanstart/redis:latest
```
---

🔹 Variants

CleanStart provides two image variants:

redis:latest → Minimal runtime variant for production security.
redis:latest-dev → Development variant with additional tools.
📥 Pull a Specific Variant

🔹 Minimal runtime variant:

```
docker pull cleanstart/redis:latest
```
🔹 Development Variant:

```
docker pull cleanstart/redis:latest-dev
```

---

🛠️ Usage Examples

💻 Getting Set Up
Redis Version
This command pulls the cleanstart/redis image to your local system and runs redis --version to check the installed version. It ensures that Redis is set up and ready to use with Docker's default configuration.

```
docker run -d --name test-redis -p 6379:6379 cleanstart/redis:latest
```

This command maps port 6379 on your host machine to the same port inside the container, allowing Redis to be accessible through its default port.

To check the logs for errors:

```
docker logs test-redis
```
The result will show no errors, indicating that Redis is ready to accept connections.

---

Redis Functionality Tests
Test 1: Basic Storage

```
docker exec -it test-redis redis-cli SET testkey "Hello Redis"
docker exec -it test-redis redis-cli GET testkey
```
Should return: "Hello Redis"

Test 2: Persistence

```
docker restart test-redis
docker exec -it test-redis redis-cli GET testkey
```
Should return: "Hello Redis" if persistence is enabled.

Test 3: Expiration

```
docker exec -it test-redis redis-cli SET tempkey "temporary" EX 10
sleep 11
docker exec -it test-redis redis-cli GET tempkey
```
Should return: (nil) after waiting.

---

Redis Networking Tests
Test 1: Port Verification

```
docker exec -it test-redis netstat -tulnp | grep 6379
```

Confirms Redis is listening on port 6379 (expect: 0.0.0.0:6379).

Test 2: Local Connectivity

```
redis-cli -h localhost -p 6379 PING
```
Verifies host machine can connect (expect: PONG).

Test 3: Container Communication

```
docker network create redis-net
docker run -d --name redis-container --network redis-net redis
docker run --rm --network redis-net redis redis-cli -h redis-container PING
```
Tests container-to-container communication (expect: PONG).

If you've successfully completed all the tests with the expected results, your Redis Docker container is fully operational and properly configured! ✅

---

🔧 Accessing a Shell in the -dev Variant

```
docker run --rm -it --entrypoint /bin/sh cleanstart/redis:latest-dev
```
⚠️ Running as Root (for Configuration Modifications)

```
docker run -it --user root --entrypoint /bin/sh cleanstart/redis:latest
```
📌 Note: Running as root is not recommended in production.

---

**Docker Hub Repository**

This image is available on Docker Hub: https://hub.docker.com/repository/docker/cleanstart/redis
