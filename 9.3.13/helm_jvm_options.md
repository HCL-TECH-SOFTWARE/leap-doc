# JVM options { #helm_jvn_options .concept }

JVM options can be specified by passing them as environment variables.

!!!note
    The max size must be calculated based on the amount needed to support the peak transactional volume.  This value may need to be adjusted if the peak load on the server increases. The minimum recommended value is 2GB.

The snippet below sets the maximum jvm memory usage to 2GB.

```yaml
environment:
   pod:
     leap:
       name:  JVM_ARGS
       value: "-Xmx2048m"
```

**Parent topic:** [Preparation](helm_preparation.md)

