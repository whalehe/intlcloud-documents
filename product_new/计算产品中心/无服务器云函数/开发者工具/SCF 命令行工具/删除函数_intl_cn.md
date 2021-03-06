SCF CLI 可以通过 `scf function delete` 命令删除已部署至云端的函数。

## 参数说明
`scf function delete` 命令支持的参数如下：

| 参数      | 简写 | 必填 | 描述                                                         | 示例                 |
| --------- | ---- | ---- | ------------------------------------------------------------ | -------------------- |
| Name      | -n   | 是   | 函数名                                                       | -n hello_world       |
| namespace | -ns  | 否   | 指定函数所在命名空间                                         | -ns  test-ns         |
| region    | -r   | 否   | 指定函数所在区域，可参见 <a href="https://intl.cloud.tencent.com/document/product/583/17238#Region-List">地域列表</a> | -r ap-shanghai |
| Force     | -f   | 否   | 强制删除                                                     | 无                   |

> 
>- 当不指定 region 和 namespace 时，默认使用 configure 里的 region 和 default 命名空间 。
> - 可执行 `scf configure get` 查看 configure 配置信息。

## 使用示例
- 执行以下命令，删除默认配置（北京区域，default 命名空间）下的指定函数。
```bash
$ scf function delete -n hello_world_delete
[>] Function Information:
[>]   Region: ap-beijing
[>]   Namespace: default
[>]   Function Name: hello_world_delete
[!] Are you sure delete this remote function? (y/n): y
[o] Function hello_world_delete delete success
```


- 执行以下命令，强制删除上海区域，default 命名空间下的指定函数。
> ! 使用强制删除参数时，将不会提示是否确认删除，请谨慎使用。
>
```bash
$ scf function delete -n test -r ap-shanghai -ns default -f
[>] Function Information:
[>]   Region: ap-shanghai
[>]   Namespace: default
[>]   Function Name: test
[o] Function deletedelete delete success
```
