# HelmChart ToTo

将 Helm Chart 推送到 [藏云阁 Harbor](https://harbor.cncfstack.com) 中，加速国内访问。

## 使用说明

以 `csi-driver-nfs-4.11.0.tgz` 为例

1、 获取 HelmChart 下载文件

注意如果是 Github，需要填写 RAW 的原始文件地址

```bash
https://github.com/kubernetes-csi/csi-driver-nfs/raw/refs/heads/master/charts/v4.11.0/csi-driver-nfs-4.11.0.tgz
```

2、 创建 PR，将 HelmChart 的下载文件 URL 填入 `helmchart.list` 中，每条一行。

3、 在 PR 合并后，会自动触发 Action 将仓库中的 HelmChart 推送到 Harbor 中。

4、 在 `https://harbor.cncfstack.com/harbor/projects/99/repositories` 中可以查看 HelmChart。（Harbor默认公开的的仓库查看也需要登录，可以注册一个账号；但是知道地址，不注册也可以下载）


5、 登录 Harbor

用户名密码可以使用交互式方式

```shell
helm registry login harbor.cncfstack.com --username <NAME> --password <PWD>
```

6、下载 Helm Chart tgz 包

```shell
% helm pull oci://harbor.cncfstack.com/helmchart/csi-driver-nfs --version 4.11.0
Pulled: harbor.cncfstack.com/helmchart/csi-driver-nfs:4.11.0
Digest: sha256:6b4125ca8b291a2723a6e7b95eac42e7b9abf2556901763150ad943965c79c42
```

7、安装 Helm Chart 

```shell
helm install MyRelease oci://harbor.cncfstack.com/helmchart/demo --version 0.1.0
```

8、 上传 Helm Chart

```shell
% helm push ~/Downloads/csi-driver-nfs-4.11.0.tgz oci://harbor.cncfstack.com/helmchart
Pushed: harbor.cncfstack.com/helmchart/csi-driver-nfs:4.11.0
Digest: sha256:6b4125ca8b291a2723a6e7b95eac42e7b9abf2556901763150ad943965c79c42
```

## 原理说明

- [Harbor 存储 HelmChart 说明](https://goharbor.io/docs/edge/working-with-projects/working-with-oci/working-with-helm-oci-charts/)


