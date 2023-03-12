## PowerShell 中使用代理

```shell
$env:HTTP_PROXY="http://127.0.0.1:10809"
$env:HTTPS_PROXY="http://127.0.0.1:10809"

# 精简成一行：
$ENV:ALL_PROXY ='http://127.0.0.1:1088'

### ！只在当前终端中生效，如果想永久生效，请在环境变量中设置
```

status = 3
product_id in (select id form fa_vip_product where brand_id = 2)