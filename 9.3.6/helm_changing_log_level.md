# Changing the log level {#helm_changing_log_level .concept}

Sometimes you may need to increase the log level to troubleshoot unexpected behavior.

Below is an example of how to change the log level.

```yaml
logging:
  leap:
    level: Leap:*=detail:com.ibm.form.nitro.*=finest
```

**Parent topic:** [Preparation](helm_preparation.md)

