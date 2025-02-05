
> 注：当前项目为 Serverless Devs 应用，由于应用中会存在需要初始化才可运行的变量（例如应用部署地区、函数名等等），所以**不推荐**直接 Clone 本仓库到本地进行部署或直接复制 s.yaml 使用，**强烈推荐**通过 `s init ${模版名称}` 的方法或应用中心进行初始化，详情可参考[部署 & 体验](#部署--体验) 。

# start-unzip-oss-v3 帮助文档

<description>

本案例是将解压zip文件工具 unzip，快速创建并部署到阿里云函数计算 FC。

</description>

<codeUrl>



</codeUrl>
<preview>



</preview>


## 前期准备

使用该项目，您需要有开通以下服务并拥有对应权限：

<service>



| 服务/业务 |  权限  | 相关文档 |
| --- |  --- | --- |
| 函数计算 |  AliyunFCFullAccess | [帮助文档](https://help.aliyun.com/product/2508973.html) [计费文档](https://help.aliyun.com/document_detail/2512928.html) |
| 对象存储 |  AliyunOSSFullAccess | [帮助文档](https://help.aliyun.com/zh/oss) [计费文档](https://help.aliyun.com/zh/oss/product-overview/billing) |

</service>

<remark>



</remark>

<disclaimers>



</disclaimers>

## 部署 & 体验

<appcenter>
   
- :fire: 通过 [Serverless 应用中心](https://fcnext.console.aliyun.com/applications/create?template=start-unzip-oss-v3) ，
  [![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://fcnext.console.aliyun.com/applications/create?template=start-unzip-oss-v3) 该应用。
   
</appcenter>
<deploy>
    
- 通过 [Serverless Devs Cli](https://docs.serverless-devs.com/user-guide/install) 进行部署：
  - [安装 Serverless Devs Cli 开发者工具](https://docs.serverless-devs.com/user-guide/install) ，并进行[授权信息配置]( https://docs.serverless-devs.com/user-guide/config) ；
  - 初始化项目：`s init start-unzip-oss-v3 -d start-unzip-oss-v3`
  - 进入项目，并进行项目部署：`cd start-unzip-oss-v3 && s deploy -y`
   
</deploy>

## 案例介绍

<appdetail id="flushContent">

本案例是将zip文件进行 unzip 解压，快速创建并部署到阿里云函数计算 FC。

匹配解压规则的ZIP文件在上传到OSS后，会自动触发函数计算进行解压。文件解压完成后，会存储至OSS的指定目录中。

- 建议使用 UTF-8 或 GB 2312 编码命名您的文件或文件夹，否则可能会出现解压后的文件或文件夹名称出现乱码、解压过程中断等问题。

- 归档或冷归档类型的文件需先解冻再解压。

- 建议 ZIP 包 + zip包里面最大单文件的大小之和不要超过 10 GB，否则解压失败。如果出现这个场景， 请参考：[unzip-oss-with-nas](https://github.com/zhaohang88/unzip-oss-nas)

- 默认设置的函数执行时长为6小时， 如果不满足需求， 自己直接调整函数的 timeout,  最大可到 24小时

    ![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5901957271/CAEQNBiBgMCKx9z24RgiIGMyMTE2ZDczNmNkYjQ2ZmI4MDNkYmYwMDIyZWE0ODkx3963382_20230830144006.372.svg)

</appdetail>

## 使用流程

<usedetail id="flushContent">

### 查看部署的案例

部署时， 选择的OSS存储桶名，以及前缀名，如：

![](https://img.alicdn.com/imgextra/i4/O1CN01KYL4lB1Obdl63LB39_!!6000000001724-0-tps-2336-1108.jpg)


部署完成后，在oss对象存储中找到相应的OSS存储桶名，向该存储桶上传zip文件，如：

![](https://img.alicdn.com/imgextra/i2/O1CN01ew8GAi1pDomkNrcuC_!!6000000005327-0-tps-1874-850.jpg)

在控制台就可以查看到调用日志，如：

![](https://img.alicdn.com/imgextra/i4/O1CN01Yv7Jsc1UJfur6G0WU_!!6000000002497-0-tps-2842-776.jpg)

#### 参数说明

![](https://img.alicdn.com/imgextra/i3/O1CN014DqNwc1jgmBgXBzqW_!!6000000004578-0-tps-1592-760.jpg)

#### 配置示例
![](https://img.alicdn.com/imgextra/i4/O1CN01WYPc2X1wcjhUAXa65_!!6000000006329-0-tps-1596-876.jpg)


### 二次开发
您可以通过云端控制台的开发功能进行二次开发。如果您之前是在本地创建的项目案例，也可以在本地项目目录`start-unzip-oss-v3`文件夹下，对项目进行二次开发。开发完成后，可以通过`s deploy`进行快速部署。

上面的示例, 解压保存回去的都还是本身触发函数的 OSS， 如果是保存到其他 OSS， 直接将 `bucket.put_object(newKey + name, file_obj)` 这样上传回 oss 的代码修改下即可， 比如：

```python
auth = oss2.Auth('<yourAccessKeyId>', '<yourAccessKeySecret>')
dst_bucket_name = "xxx-bucket"
dst_bucket = oss2.Bucket(auth, endpoint, dst_bucket_name)
dst_bucket.put_object(newKey +  name, file_obj)

```

</usedetail>

## 注意事项

<matters id="flushContent">
</matters>


<devgroup>


## 开发者社区

您如果有关于错误的反馈或者未来的期待，您可以在 [Serverless Devs repo Issues](https://github.com/serverless-devs/serverless-devs/issues) 中进行反馈和交流。如果您想要加入我们的讨论组或者了解 FC 组件的最新动态，您可以通过以下渠道进行：

<p align="center">  

| <img src="https://img.alicdn.com/imgextra/i2/O1CN010Sk7sv1Xl6WuOb6uU_!!6000000002963-0-tps-666-662.jpg" width="130px" > | <img src="https://img.alicdn.com/imgextra/i4/O1CN010Vt5aw27VN5rJIguB_!!6000000007802-0-tps-668-630.jpg" width="130px" > |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| <center>微信公众号：`serverless`</center>                                                                                         | <center>钉钉交流群：`33947367`</center>                                                                                           |
</p>
</devgroup>
