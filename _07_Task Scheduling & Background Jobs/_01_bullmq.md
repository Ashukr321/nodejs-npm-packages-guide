# _01_ BullMQ

BullMQ is a Node.js message queue library for handling distributed jobs and messages based on Redis.

## 🚀 Why use BullMQ?
- **Robustness:** Built on top of Redis, it handles persistence and crashes gracefully.
- **Features:** Supports delayed jobs, priorities, parent-child dependencies, and retries.
- **UI:** Integration with BullBoard for visual monitoring.

## 🛠️ Integration Steps

### Step 1: Installation
```bash
npm install bullmq ioredis
```

### Step 2: Queue Setup
Create a Queue, a Worker, and a FlowProducer.

## 💻 Code Sample

```javascript
const { Queue, Worker } = require('bullmq');

// 1. Create Queue
const emailQueue = new Queue('emails', {
  connection: { host: 'localhost', port: 6379 }
});

// 2. Add Job to Queue
async function addEmailJob(data) {
  await emailQueue.add('sendWelcomeEmail', data, {
    delay: 5000, // Send after 5 seconds
    attempts: 3
  });
}

// 3. Create Worker to Process Jobs
const worker = new Worker('emails', async job => {
  if (job.name === 'sendWelcomeEmail') {
    console.log(`📧 Sending email to ${job.data.email}...`);
    // Logic to send email via Nodemailer
  }
}, {
  connection: { host: 'localhost', port: 6379 }
});

worker.on('completed', job => console.log(`✅ Job ${job.id} completed`));
worker.on('failed', (job, err) => console.error(`❌ Job ${job.id} failed: ${err.message}`));
```
