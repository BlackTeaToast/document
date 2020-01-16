# KeyVaultʹ��˵��

KeyVault����������ȫ�ش洢������Ϣ����������ʽ����ϸ���ơ�

##  Ȩ����֤

KeyVaultʹ��SSO��Ȩ����֤���ƣ�����ʹ��KeyVault��API֮ǰ����Ҫ��һ��SSO�˻����е�¼��Ȼ��ȡ�õ�¼��Token��֮������ʹ��Token����KeyVault��API��



## ����KeyVault

�û����ӵ��ĳ��Namespace��Ȩ�ޣ�����Ը���ǰNamespace����һ��KeyVaultʵ����������ν��ʵ������ʵ����һ�����ڴ洢Secret��·����

Method

```
POST /secret/cluster/{clusterName}/namespace/{namespaceName}
```

����˵�����£�

| Name | Value                                                        |
| ---- | ------------------------------------------------------------ |
| clusterName   | cluster������                               |
| NamespaceName   | namespace������ |

���ز���json��ʽ���£�

```
{
	"id": "<string>",
	"subscriptionId": "<string>",
	"isValidTransaction": <bool>,
	"number": <integer>,
	"authcode": "<string>",
	"activeInfo": "<string>"
}
```

����˵�����£�

| Name               | Value                                                     |
| ------------------ | --------------------------------------------------------- |
| id                 | ����ʵ��id����serviceInstanceId                           |
| subscriptionId     | ���ĺ�id                                                  |
| isValidTransaction | �û�����״̬��true=��Ч��false=��Ч����Ϊ��Чʱ������ʧ�� |
| number             | ���ĵ��Ϻ���������pnQuantity                              |
| authcode           | ������                                                    |
| activeInfo         | �����ϼ�ʱ�Զ���ļ�����Ϣ                                |

������

* Request Example:
  http://api-license-master.internal/v1/api/partNum/licenseQty?pn=9806WPAFS0&id=9ca0b70f-3357-11ea-beb1-76a42f50fd69

* Response Example:

  ```
  {
  	id: "9ca0b70f-3357-11ea-beb1-76a42f50fd69", //����ʵ��id
  	subscriptionId: "ff4fbd21-5962-4427-88a0-b8ef4ac9b393", //���ĺ�id
  	isValidTransaction: true,  //�û�����״̬��true=��Ч��false=��Ч
  	number: 120,   // ���ĵ��Ϻ�����
  	authcode: "3080-e825-003c",  
  	activeInfo: ""  //�����ϼ�ʱ�Զ���ļ�����Ϣ
  }
  
  ```



## ���Secrets

������ĳ��Namespace��KeyVault֮�󣬱���Խ���ǰNamespace��secret������Ӧ��·�����档Namespace·����������ٿ���·��������ͼ�е�subPath��subPath֧�ֵ�������Ϊ10��subPath����洢�����secret��ÿ��subPath�洢secret�����Ϊ100KB��

```
|-- NamespacePath
|   |-- subPath1
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath2
|   |   |  key1: vaule1
|   |-- subPath3
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath4
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath5
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath6
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath7
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath8
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath9
|   |   |  key1: vaule1
|   |   |  key2: vaule2
|   |-- subPath10
|   |   |  key1: vaule1
|   |   |  key2: vaule2
```

Method

```
POST /secret/cluster/{clusterName}/namespace/{namespaceName}/path/{path}
```

Request body��

```
{
  "data":{
    "key1":"vaule1",
    "key2":"vaule2"
  }
}
```
����˵�����£�

| Name | Value                                                        |
| ---- | ------------------------------------------------------------ |
| clusterName   | cluster������                               |
| NamespaceName   | namespace������ |
| path   | path������ |
| data   | secret��key��vaule��֧�ֶ���key��vaule |



## ��ȡSecrets



Method

```
GET /secret/cluster/{clusterName}/namespace/{namespaceName}/path/{path}
```

����˵�����£�

| Name | Value                                                        |
| ---- | ------------------------------------------------------------ |
| clusterName   | cluster������                               |
| NamespaceName   | namespace������ |
| path   | path������ |
| data   | secret��key��vaule��֧�ֶ���key��vaule |


## Ӧ�ó����ȡSecrets

��Secrets��ӳɹ���Ӧ�ó������ͨ��ע��Sidecar�ķ�ʽ��ȡSecrets��ֵ��ʹ�ô˷�ʽ֮��Ӧ�ó�����Բ��ù�ע��ô��ȡSecrets�Ĺ��̣����գ�ֻ��Ҫ���ĺ��ٵĴ��룬������õ���Ҫ��Secrets��

ע��ɹ�֮��Pod�л���һ��Container����Ϊconsul-template����Container����Secrets��ֵ��ȡ������Ȼ���Թ����ķ�ʽ�����Ӧ�ó������container����ˣ���Ӧ�ó������container�£�����һ��vault-secrets.txt�ļ������ļ�λ��/etc/sectets���棬�ļ������ݾ���key��vaule�ļ�ֵ�ԡ�

Method

```
POST /secret/cluster/{clusterName}/namespace/{namespaceName}/deployment/{deploymentName}
```

Request body��

```

[
	{
		"path":"subPath1",
		"keys":["key1", "key2"]
	},
	{
		"path":"subPath2",
		"keys":["key1"]
	}
]
```
����˵�����£�

| Name | Value                                                        |
| ---- | ------------------------------------------------------------ |
| clusterName   | cluster������                               |
| NamespaceName   | namespace������ |
| deployment   | ��Ҫ����ע���deployment������ |
| path   | namespace����·�������ƣ�֧�ֶ��� |
| keys   | namespace����·���´洢��secrets��keyֵ��֧�ֶ��� |


