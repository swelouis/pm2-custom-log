# Introduction

This a is custom PM2 module for sending events & logs from your PM2 processes to Discord

# How to install & run

```
  git clone https://github.com/swelouis/pm2-custom-log
  npm i
  pm2 start ecosystem.config.json
  pm2 set pm2-custom-log:discord_url https://discord_url
```

# Configure

The following events can be subscribed to:

-   log - All standard out logs from your processes. Default: false
-   error - All error logs from your processes. Default: true
-   kill - Event fired when PM2 is killed. Default: true
-   exception - Any exceptions from your processes. Default: true
-   restart - Event fired when a process is restarted. Default: true
-   delete - Event fired when a process is removed from PM2. Default: false
-   stop - Event fired when a process is stopped. Default: true
-   restart overlimit - Event fired when a process is reaches the max amount of times it can restart. Default: true
-   exit - Event fired when a process is exited. Default: false
-   start - Event fired when a process is started. Default: false
-   online - Event fired when a process is online. Default: false

You can simply turn these on and off by setting them to true or false using the PM2 set command.

```
  pm2 set pm2-custom-log:log true
```

## Options

The following options are available:

-   **process_name** (string): When this is set, it outputs only the logs of specific named processes. Default: NULL. You can specify multiple process names separated by commas, e.g., `service_1, service_2`
-   **without_keywords** (string): When this is set, it excludes logs containing specific keywords in the message. You can specify multiple process names separated by commas, e.g., `error_1,health-check`
-   **include_keywords** (string): When this is set, it outputs only the logs containing specific keywords in the message. You can specify multiple keywords separated by commas, e.g., `error_1,health-check`
-   **buffer** (bool) - Enable/Disable buffering of messages by timestamp. Messages that occur with the same timestamp (seconds) will be concatenated together and posted as a single discord message. `Default: true`
-   **buffer_seconds** (int) - Duration in seconds to aggregate messages. Has no effect if buffer is set to false. `Min: 1, Max: 5, Default: 1`
-   **queue_max** (int) - Number of messages to keep queued before the queue will be truncated. When the queue exceeds this maximum, a rate limit message will be posted to discord. `Min: 10, Max: 100, Default: 100`

Set these options in the same way you subscribe to events.

Example: The following configuration options will enable message buffering, and set the buffer duration to 2 seconds. All messages that occur within 2 seconds of each other (for the same event) will be concatenated into a single discord message.

```
pm2 set pm2-discord:process_name myprocess
pm2 set pm2-discord:buffer true
pm2 set pm2-discord:buffer_seconds 2
pm2 set pm2-discord:queue_max 50
```

## Contributing

-   I'm contributing from this ![repo](https://github.com/FranciscoG/pm2-discord)
