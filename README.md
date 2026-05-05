# Assignment-3-Server-and-client

This repository contains my solution for Assignment 3 – Server-Client Communication using the STOMP protocol.  
The project implements a full messaging system with a Java server and a C++ client.

Java & C++ -- STOMP Messaging System
Implementation of a multi-client server and client using the STOMP (Simple Text Oriented Messaging Protocol).

---

Overview

This project implements a **community-driven World Cup update system** where users:

- Connect to a server
- Subscribe to game channels
- Send and receive real-time updates
- Maintain local summaries of game events

The system is based on the STOMP messaging protocol and supports multiple concurrent clients.

According to the assignment description :contentReference[oaicite:0]{index=0}, the system enables clients to subscribe to topics and exchange messages via a central server.

---

Implemented Features

1. STOMP Server (Java)

- Supports two server models:
  - Thread-Per-Client (TPC)
  - Reactor pattern

Core components:
- Connections manager (client tracking)
- Connection handlers
- STOMP protocol implementation

Features:
- Topic-based publish/subscribe system
- Message broadcasting to subscribers
- Client authentication (login/password)
- Error handling via ERROR frames
- Graceful disconnection with RECEIPT frames

---

2. STOMP Protocol Implementation

Supported client frames:
- CONNECT
- SEND
- SUBSCRIBE
- UNSUBSCRIBE
- DISCONNECT

Supported server frames:
- CONNECTED
- MESSAGE
- RECEIPT
- ERROR

Features:
- Full frame parsing (headers + body)
- Topic-based message routing
- Subscription management per client
- Unique message and subscription IDs

---

3. Client (C++)

- Multi-threaded client:
  - Thread 1: reads user input (keyboard)
  - Thread 2: listens to server messages

Supported commands:
- login {host:port} {username} {password}
- join {game_name}
- exit {game_name}
- report {file}
- summary {game_name} {user} {file}
- logout

Features:
- Converts user commands into STOMP frames
- Parses incoming frames from server
- Maintains local state of game updates
- Handles graceful disconnect

---

4. Game Event System

- Users report game updates via JSON files
- Events include:
  - Event name
  - Time
  - Game statistics
  - Description

Features:
- Sends each event as a message to a topic
- Stores events per user and per game
- Supports generating summaries of matches

---

5. Concurrency & Synchronization

- Server handles multiple clients concurrently
- Safe message distribution across topics
- Client uses threads to avoid blocking

Focus:
- Thread-safe communication
- Efficient handling of multiple connections

---

Build & Run

Server (Java with Maven):

mvn compile

Run TPC server:
mvn exec:java -Dexec.mainClass="bgu.spl.net.impl.stomp.StompServer" -Dexec.args="<port> tpc"

Run Reactor server:
mvn exec:java -Dexec.mainClass="bgu.spl.net.impl.stomp.StompServer" -Dexec.args="<port> reactor"

---

Client (C++):

make

Run:
./bin/StompWCIClient

---

Environment

Java (Maven)
C++
Linux / WSL

---

Notes

- Focus on networking and protocol implementation
- Demonstrates client-server architecture
- Combines Java backend with C++ frontend
- Implements real-world messaging protocol (STOMP)
- Emphasis on concurrency, parsing, and system design
