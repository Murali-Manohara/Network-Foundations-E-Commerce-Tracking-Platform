# 🚚 Scalable Real-Time Order Tracking System

A distributed, event-driven architecture designed for a fast-growing e-commerce platform to provide **fast, reliable, secure, and real-time order tracking**, even during sudden traffic spikes and major sales events.

---

## 📌 Problem Statement

As order volumes increase, an e-commerce platform may experience:

- ⏳ Delayed order-status updates
- ❌ Missed status changes
- 🚨 High traffic during major sales
- 🐌 Slow tracking responses
- 🔄 Unreliable real-time updates

The goal is to design an architecture that can scale horizontally while maintaining reliability, security, and low latency.

---

## 🏗️ Architecture

```text
                         CUSTOMER
                            |
                         HTTPS/WSS
                            |
                            ↓
                    +----------------+
                    | LOAD BALANCER  |
                    +-------+--------+
                            |
                            ↓
                     API GATEWAY
                            |
                          gRPC
                            |
                            ↓
                    +----------------+
                    | ORDER SERVICE  |
                    +-------+--------+
                            |
                     +------+------+
                     |             |
                     ↓             ↓
                   CACHE       DATABASE
                     |
                     |
                Order Status Event
                     |
                     ↓
                    KAFKA
                 /         \
                ↓           ↓
       TRACKING SERVICE   NOTIFICATION
          CONSUMERS         SERVICE
              |                |
              ↓                ↓
          WebSocket       Push/SMS/Email
              |
              ↓
           CUSTOMER
