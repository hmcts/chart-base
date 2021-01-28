# chart-base

Base Helm chart for all applications.

It adds below templates from [chart-library](https://github.com/hmcts/chart-library/) based on the chosen configuration:

- [Deployment](https://github.com/hmcts/chart-library/tree/master#deployment)
- [Horizontal Pod Auto Scaler](https://github.com/hmcts/chart-library/tree/master#hpa-horizontal-pod-auto-scaler)
- [Ingress](https://github.com/hmcts/chart-library/tree/master#ingress)
- [Pod Disruption Budget](https://github.com/hmcts/chart-library/tree/master#pod-disruption-budget)
- [Service](https://github.com/hmcts/chart-library/tree/master#service)
- [Deployment Tests](https://github.com/hmcts/chart-library/tree/master#smoke-and-functional-tests)

## Language Settings

As detailed in [chart-library](https://github.com/hmcts/chart-library/tree/master#language), applications can set `language` property to pick sensible defaults for a particular language.

Example:
```
language: java
```
will override values from defaults with
```
java:
  key1: value1
  key2: value2
  key3: value3
``` 

## Configuration defaults

- Check [values.yaml](base/values.yaml) for default configuration.
- Values defined under `language:` takes priority over base defaults.
- Check additional configuration options for each template from [chart-library](https://github.com/hmcts/chart-library/)
- If, values are configured for a specific language, they can only be overridden in language level.

  If [values.yaml](base/values.yaml) have defaults like below: 
  
  ```yaml
  replicas: 1
  java:
    memoryRequests: '512Mi'
  ```
  An application chart configured below 
  ```yaml
  base:
    language: java
    replicas: 2
    memoryRequests: '1024Mi'
  ```
  will set replicas to `2` , **but memoryRequests will still be `512Mi`**. It can be set `1024Mi` by using below config
  
  ```yaml
    base:
      language: java
      replicas: 2
      java:
        memoryRequests: '1024Mi'
    ```