the perimeter simplified service development while keeping inter-service authentication overhead below 3 milliseconds."*

---

## 3. Deep-Dive Answers to Follow-Up Technical Questions

### Q1: How do you handle database schema migrations when executing zero-downtime microservice updates?
> **Answer:** *"Database schema updates must be completely decoupled from code deployments by applying the **Expand-Contract Pattern**:
> 1. **Expand Step:** Execute backward-compatible, additive database updates (e.g., introducing a new column or table without removing existing ones).
> 2. **Deploy Step:** Deploy the updated microservice code, configured to read from and write to both old and new schema structures.
> 3. **Migrate & Contract Step:** Run data backfill scripts to align legacy records, transition readers to the new schema, and subsequently remove legacy database structures in a secondary release once the updated code is fully stabilized."*

### Q2: JWTs are stateless. How do you revoke or invalidate a JWT token prior to its expiration time across microservices?
> **Answer:** *"While keeping short access token lifetimes (e.g., 5–15 minutes) paired with refresh tokens is the standard approach, immediate revocation is achieved through:
> 1. **API Gateway Blacklisting:** Maintaining a high-throughput distributed memory store (**Redis**) at the API Gateway to validate incoming token identifiers (`jti`) against an active revocation list.
> 2. **Event-Driven Revocation Broadcasting:** Emitting real-time token revocation events over a message bus (Kafka/RabbitMQ) upon user logout or security trigger events, allowing microservices to update short-lived local in-memory validation caches."*
