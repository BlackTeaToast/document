# KeyVaultʹ��˵��

KeyVault����������ȫ�ش洢������Ϣ����������ʽ����ϸ���ơ�

## Step 1��

*  Ȩ����֤

KeyVaultʹ��SSO��Ȩ����֤���ƣ�����ʹ��KeyVault��API֮ǰ����Ҫ��һ��SSO�˻����е�¼��Ȼ��ȡ�õ�¼��Token��֮������ʹ��Token����KeyVault��API��

## Step 2��

* ����KeyVault

�û�Ҫʹ��KeyVault֮ǰ����Ҫ����һ��KeyVaultʵ����������ν��ʵ������ʵ����һ�����û�ID���������ڴ洢Secret��·����

Method
```
POST /secret
```
������KeyVaultʵ��֮�󣬿���ͨ��GET�鿴��

Method
```
GET /secret
```
������ȡ�����ģ�����������Ҫע��һ�㣬����û�ȡ������֮�󣬵�ǰ����û��洢������secret���ᱻɾ����

Method
```
DELETE /secret
```
## Step 3��

* ���Secrets

�û�������KeyVault֮�󣬱���Խ�secret�洢�ڵ�ǰ·�����档UserId·����������ٿ���·��������ͼ�е�subPath��subPath֧�ֵ�������Ϊ10��subPath����洢�����secret��ÿ��subPath�洢secret�����Ϊ100KB��

```
|-- UserId
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
POST /secret/path/{path}
```


�����secrets֮����Բ鿴


Method

```
GET /secret/path/{path}
```
Ҳ����ɾ���û�ĳ����·���µ�secrets

Method

```
DELETE /secret/path/{path}
```

## Step 4��

* Ӧ�ó����ȡSecrets

��Secrets��ӳɹ���Ӧ�ó������ͨ��ע��Sidecar�ķ�ʽ��ȡSecrets��ֵ��ʹ�ô˷�ʽ֮��Ӧ�ó�����Բ��ù�ע��ô��ȡSecrets�Ĺ��̣����գ�ֻ��Ҫ���ĺ��ٵĴ��룬������õ���Ҫ��Secrets��

ע��ɹ�֮��Pod�л���һ��Container����Ϊconsul-template����Container����Secrets��ֵ��ȡ������Ȼ���Թ����ķ�ʽ�����Ӧ�ó������container����ˣ���Ӧ�ó������container�£�����һ��vault-secrets.txt�ļ������ļ�λ��/etc/sectets���棬�ļ������ݾ���key��vaule�ļ�ֵ�ԡ�

Method

```
PUT /secret/cluster/{clusterName}/namespace/{namespaceName}/deployment/{deploymentName}
```
ע��֮�󣬿��Բ鿴ע���Ƿ�ɹ�

Method

```
GET /secret/cluster/{clusterName}/namespace/{namespaceName}/deployment/{deploymentName}
```
Ҳ���Զ�ע���container���г���
```
DELETE /secret/cluster/{clusterName}/namespace/{namespaceName}/deployment/{deploymentName}
```

## ע������
* ���ɾ����ĳ��secret���������secret֮ǰ�Ѿ���ע�뵽��deployment�У�deployment����Ϊ�Ҳ������secret����������������ϣ����ɾ����ĳ��secret֮�󣬿���ͬʱ����ע��container��secret

