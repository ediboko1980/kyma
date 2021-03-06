---
title: Environment variables
type: Configuration
---

To configure the Function with the Node.js runtime, override the default values of these environment variables:

| Environment variable | Description                                                               | Type   | Default value |
| -------------------- | ------------------------------------------------------------------------- | ------ | ------------- |
| **FUNC_TIMEOUT**     | Specifies the number of seconds in which a runtime must execute the code. | Number | `180`         |
| **REQ_MB_LIMIT**     | Specifies the payload body size limit in megabytes.                       | Number | `1`           |

See [`kubeless.js`](https://github.com/kubeless/runtimes/blob/master/stable/nodejs/kubeless.js) to get a deeper understanding of how the Express server, that acts as a runtime, uses these values internally to run Node.js Functions.

See the example of a Function with these environment variables set:

```yaml
apiVersion: serverless.kyma-project.io/v1alpha1
kind: Function
metadata:
  name: sample-fn-with-envs
  namespace: default
spec:
  env:
    - name: FUNC_TIMEOUT
      value: "2"
    - name: REQ_MB_LIMIT
      value: "10"
  source: |
    module.exports = {
      main: function (event, context) {
        return "Hello World!";
      }
    }
```

To configure a Function with the Python runtime, override the default values of these environment variables:

| Environment variable | Description                                      | Unit   | Default value   |
| -------------------- | ------------------------------------------------ | ------ | --------------- |
| **FUNC_MEMFILE_MAX** | Maximum size of memory buffer for the HTTP request body in bytes. | Number | `100*1024*1024` | <!-- https://bottlepy.org/docs/dev/api.html#bottle.BaseRequest.MEMFILE_MAX --> |

See [`kubeless.py`](https://github.com/kubeless/runtimes/blob/master/stable/python/_kubeless.py) to get a deeper understanding of how the Bottle server, that acts as a runtime, uses these values internally to run Python Functions.

```yaml
apiVersion: serverless.kyma-project.io/v1alpha1
kind: Function
metadata:
  name: sample-fn-with-envs
  namespace: default
spec:
  env:
    - name: FUNC_MEMFILE_MAX
      value: "1048576" # 1MiB
  source: |
    def main(event. context):
      return "Hello World!"
```
