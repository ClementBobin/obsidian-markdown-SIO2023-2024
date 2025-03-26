## Overview

PM2 is a powerful process manager for Node.js applications that helps manage and monitor processes in production environments. It ensures that applications remain alive, can restart automatically if they crash, and provides insightful metrics on performance.

## Why Use PM2?

- **Automatic Restarts**: Keeps your applications running by automatically restarting crashed processes.
    
- **Load Balancing**: Supports clustering to distribute traffic across multiple instances.
    
- **Log Management**: Aggregates and manages logs efficiently.
    
- **Monitoring & Metrics**: Provides a built-in dashboard for real-time monitoring.
    
- **Process Scaling**: Easily scales applications across multiple CPU cores.
    
- **Deployment Workflow**: Simplifies application deployment with a built-in process for handling updates.
    

---

## Installation

To install PM2 globally, run:

```sh
npm install -g pm2
```

To verify installation:

```sh
npm list -g pm2
```

---

## Basic Usage

### Start an Application

```sh
pm start pm2 start app.js
```

This starts the `app.js` file as a PM2-managed process.

### List Running Processes

```sh
pm start pm2 list
```

Shows a table with information about all managed processes.

### Restart a Process

```sh
pm start pm2 restart app
```

Restarts the process named `app`.

### Stop and Delete a Process

```sh
pm start pm2 stop app
pm start pm2 delete app
```

Stops and removes the process from PM2.

### Auto Restart on System Boot

To ensure PM2 restarts applications when the system reboots, run:

```sh
pm start pm2 startup
```

Then follow the instructions to enable the startup script.

### Logging

To view application logs in real-time:

```sh
pm start pm2 logs
```

To filter logs for a specific process:

```sh
pm start pm2 logs app
```

To flush logs and clear all stored log data:

```sh
pm start pm2 flush
```

### Process Scaling

To start multiple instances of an application using all available CPU cores:

```sh
pm start pm2 start app.js -i max
```

Or specify the number of instances:

```sh
pm start pm2 start app.js -i 4
```

### Monitoring

For a real-time dashboard:

```sh
pm start pm2 monit
```

This provides CPU, memory, and process status updates.

### Save and Restore Process List

To save the current list of processes:

```sh
pm start pm2 save
```

To restore processes after a system reboot:

```sh
pm start pm2 resurrect
```

---

## Advanced Features

### Deployments

PM2 supports zero-downtime deployments using the following command:

```sh
npm start pm2 reload app
```

### Ecosystem Configuration

PM2 allows defining multiple applications using an `ecosystem.config.js` file. Example:

```js
module.exports = {
  apps: [
    {
      name: "my-app",
      script: "app.js",
      instances: "max",
      exec_mode: "cluster",
      env: {
        NODE_ENV: "production"
      }
    }
  ]
};
```

To start applications using this configuration:

```sh
pm start pm2 start ecosystem.config.js
```

### Deployment Workflow

PM2 provides an integrated deployment system. First, define deployment settings in `ecosystem.config.js`:

```js
module.exports = {
  apps: [
    {
      name: "my-app",
      script: "app.js",
      instances: "max",
      exec_mode: "cluster",
      env: {
        NODE_ENV: "production"
      }
    }
  ],
  deploy: {
    production: {
      user: "node",
      host: "myserver.com",
      ref: "origin/main",
      repo: "git@github.com:username/repo.git",
      path: "/var/www/my-app",
      "post-deploy": "npm install && pm2 restart ecosystem.config.js --env production"
    }
  }
};
```

To deploy the application:

```sh
pm start pm2 deploy production setup
pm start pm2 deploy production
```

---

## Conclusion

PM2 is a robust and feature-rich process manager that simplifies managing Node.js applications in production. It offers automatic restarts, monitoring, load balancing, and advanced deployment strategies. By integrating PM2 into your workflow, you can enhance the stability and performance of your applications efficiently.

## Documentation: 
[pm2](https://pm2.keymetrics.io/docs/usage/quick-start/)