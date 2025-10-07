# Changing the log level { #helm_changing_log_level .concept }

Sometimes you may need to increase the log level to troubleshoot unexpected behavior.

Below is an example of how to change the log level.

```yaml
logging:
  leap:
    level: Leap:*=detail,Leap:com.ibm.form.nitro.*=finest
```
The general format is `Leap:[packageName1].*=[level1],Leap:[packageName2].*=[level2],...`

The default log configuration is `*=info`.

See [logging levels](https://openliberty.io/docs/latest/log-trace-configuration.html#logging_levels) for more details.

**Parent topic:** [Preparation](helm_preparation.md)

