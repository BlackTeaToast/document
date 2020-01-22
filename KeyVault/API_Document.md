# Subscribe keyvault 

�û�����keyvault

| Method | Path                                                        |
| ---- | ----|
| POST   | /secret      |



### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request POST \    
    http://127.0.0.1:8200/secret
```

### Sample Response
---
```
{
  "reason": "success",
  "message": "OK",
  "code": 200
}

```
# Unsubscribe keyvault 

�û��˶�keyvault

| Method | Path                                                        |
| ---- | ----|
| DELETE   | /secret       |



### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request DELETE \    
    http://127.0.0.1:8200/secret
```

### Sample Response
---
```
{
  "reason": "success",
  "message": "OK",
  "code": 200
}

```

# Get subPath 

��ȡĳ���û���������·��

| Method | Path                                                        |
| ---- | ----|
| GET   | /secret      |



### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request GET \    
    http://127.0.0.1:8200/secret
```

### Sample Response
---
```
{
  "request_id": "6071835e-f70c-6b8a-081e-8b54bfad7f67",
  "lease_id": "",
  "lease_duration": 0,
  "renewable": false,
  "data": {
    "keys": [
      "default",
      "nginx-test"
    ]
  },
  "warnings": null
}

```

# Create Secret

���secret


| Method | Path                                                        |
| ---- | ----|
| POST   | /secret/path/{path}                               |


### Parameters
---

* <font color=Blue>path</font> (string: required) - path������
* <font color=Blue>data</font> (Map: required) - ���secret������


### Sample Payload
---
```
{
  "data":{
    "key1":"value1",
    "key2":"value2"
  }
}
```

### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request POST \
    --data @payload.json \
    http://127.0.0.1:8200/secret/path/sp-1
```

### Sample Response
---
```
{
  "request_id": "43ccec60-e38c-9f06-c899-6a41017844a6",
  "lease_id": "",
  "lease_duration": 0,
  "renewable": false,
  "data": {
    "created_time": "2020-01-16T05:25:47.985093248Z",
    "deletion_time": "",
    "destroyed": false,
    "version": 1
  },
  "warnings": null
}

```


# Get Secret
��ȡsecret


| Method | Path                                                        |
| ---- | ----|
| GET   | /secret/path/{path}                               |


### Parameters
---

* <font color=Blue>path</font> (string: required) - path������

### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request GET \  
    http://127.0.0.1:8200/secret/path/sp-1
```

### Sample Response
---
```
{
  "request_id": "e2efeeeb-7252-57e1-bde9-23e0fc799216",
  "lease_id": "",
  "lease_duration": 0,
  "renewable": false,
  "data": {
    "data": {
      "key1": "vaule1",
      "key2": "vaule2"
    },
    "metadata": {
      "created_time": "2020-01-16T05:25:47.985093248Z",
      "deletion_time": "",
      "destroyed": false,
      "version": 1
    }
  },
  "warnings": null
}

```

# Delete Secret
ɾ��secret


| Method | Path                                                        |
| ---- | ----|
| DELETE   | /secret/path/{path}                               |


### Parameters
---

* <font color=Blue>path</font> (string: required) - path������

### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request DELETE \  
    http://127.0.0.1:8200/secret/path/sp-1
```
# Inject sidecar to deployment

��deployment��Ӧ��podע��sidecar


| Method | Path                                                        |
| ---- | ----|
| PUT   | /secret/cluster/{clusterName}/namespace/{namespaceName}/deployment/{deploymentName}                               |


### Parameters
---
* <font color=Blue>clusterName</font> (string: required) - cluster������
* <font color=Blue>namespaceName</font> (string: required) - namespace������
* <font color=Blue>deploymentName</font> (string: required) - deployment������
* <font color=Blue>path</font> (string: required) - path������
* <font color=Blue>keys</font> ([]string: optional) - secret��key������


### Sample Payload
---
```
[
  {
    "keys": ["key1", "key2"],
    "path": "nginx-test"
  },
  {
    "keys": ["key1"],
    "path": "nginx-test-1"
  }
]
```

### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request PUT \
    --data @payload.json \
    http://127.0.0.1:8200/secret/cluster/c-1/namespace/ns-1/deployment/dm-1
```

### Sample Response
---
```
{
  "reason": "success",
  "message": "OK",
  "code": 200
}

```
# Remove injected container

�Ƴ�pod��ע���container


| Method | Path                                                        |
| ---- | ----|
| DELETE   | /secret/cluster/{clusterName}/namespace/{namespaceName}/deployment/{deploymentName}                               |


### Parameters
---
* <font color=Blue>clusterName</font> (string: required) - cluster������
* <font color=Blue>namespaceName</font> (string: required) - namespace������
* <font color=Blue>deploymentName</font> (string: required) - deployment������


### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request DELETE \   
    http://127.0.0.1:8200/secret/cluster/c-1/namespace/ns-1/deployment/dm-1
```

### Sample Response
---
```
{
  "reason": "success",
  "message": "OK",
  "code": 200
}

```

# Get deployment status

��ȡdeployment��pod��״̬


| Method | Path                                                        |
| ---- | ----|
| GET   | /secret/cluster/{clusterName}/namespace/{namespaceName}/deployment/{deploymentName}                               |


### Parameters
---
* <font color=Blue>clusterName</font> (string: required) - cluster������
* <font color=Blue>namespaceName</font> (string: required) - namespace������
* <font color=Blue>deploymentName</font> (string: required) - deployment������


### Sample Request
---

```
$ curl \
    --header "Authorization: Bearer .... \
    --request GET \
    http://127.0.0.1:8200/secret/cluster/c-1/namespace/ns-1/deployment/dm-1
```

### Sample Response
---
```
{
  "status": "Running"
}
```