# JVM options { #helm_jvn_options .concept }

JVM options can be specified by passing them as environment variables.

The snippet below sets the maximum jvm memory usage to 2GB.

```yaml
environment:
   pod:
     leap:
       name:  JVM_ARGS
       value: "-Xmx2048m"
```

**Parent topic:** [Preparation](helm_preparation.md)

