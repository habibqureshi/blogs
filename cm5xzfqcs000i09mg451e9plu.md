---
title: "Debug Like a Pro: Writing Logs That Solve Production Mysteries"
seoTitle: "Custom Logging"
datePublished: Wed Jan 15 2025 14:13:46 GMT+0000 (Coordinated Universal Time)
cuid: cm5xzfqcs000i09mg451e9plu
slug: debug-like-a-pro-writing-logs-that-solve-production-mysteries
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/CO6r5hbt1jg/upload/329babd4c6af2bfe7fd255d7777178a8.jpeg
tags: express, nodejs, backend, debugging, consolelog

---

Poorly written logs can leave you in the dark when trying to debug issues in your backend application. Without crucial information, pinpointing the root cause becomes nearly impossible. Bad logs turn debugging into a guessing game, wasting valuable time and escalating downtime.

---

### The Problem with Generic Logs

Consider the following logging example in a user creation workflow

```javascript
if (createUser.password) {
  createUser.password = await bcrypt.hash(createUser.password, 10);
}
console.log(`Creating user ${JSON.stringify(createUser)}`);

const newUser = this.userRepository.create(createUser);
console.log(`User created successfully ${JSON.stringify(newUser)}`);
return await this.userRepository.save(newUser, { reload: true });
```

### Output

```plaintext
Creating user {"email":"test@gmail.com","name":"test","password":"$2b$10$..."} 
User created successfully {"name":"test","password":"$2b$10$...","email":"test@gmail.com"}
```

### Problem

At first glance, these logs might seem sufficient. But as the complexity of the application grows, this approach quickly falls short. Here’s what’s missing:

1. **Timestamp** – When did this action happen?
    
2. **Source** – Which file, service, or line of code produced this log?
    
3. **User Context** – Who triggered this action?
    
4. **Request Correlation** – What is the unique request ID for tracing logs across services?
    

### Transforming Logs into Debugging Powerhouses

By including critical metadata, we can turn generic logs into **actionable insights**. Here's how the improved logs look:

```plaintext
97048 - 01/15/2025, 5:24:38 PM LOG 0b84a479-1a8e-4a95-96cf-5f31d17793a3 ::1 user@example.com 2025-01-15T12:24:38.492Z users.service.ts:17 Creating user {"email":"test@gmail.com","name":"test","password":"$2b$10$..."}
97048 - 01/15/2025, 5:24:38 PM LOG 0b84a479-1a8e-4a95-96cf-5f31d17793a3 ::1 user@example.com 2025-01-15T12:24:38.493Z users.service.ts:17 User created successfully {"name":"test","password":"$2b$10$...","email":"test@gmail.com"}
```

### Key Improvements:

1. **Timestamps**: Logs now include precise timestamps to track when events occurred.
    
2. **File and Line Number**: Identify the exact location in the codebase (e.g., `users.service.ts:17`).
    
3. **User Context**: Know who initiated the action ([`user@example.com`](mailto:user@example.com)).
    
4. **Request ID**: Trace logs across distributed systems with a unique request ID (`0b84a479-1a8e-4a95-96cf-5f31d17793a3`).
    

### Why This Matters

* **Faster Debugging**: Detailed logs allow developers to pinpoint issues quickly.
    
* **Better Collaboration**: Logs with contextual metadata (e.g., user info, request ID) make it easier for teams to reproduce and understand issues.
    
* **Proactive Monitoring**: Structured logs are easier to integrate with tools like **ELK Stack** or **Datadog**, enabling real-time monitoring and alerting.
    

I've written an example in Node.js using Log4js. Check it out at [https://github.com/habibqureshi/log4jsWithNodejs](https://github.com/habibqureshi/log4jsWithNodejs).

*Happy Debugging*