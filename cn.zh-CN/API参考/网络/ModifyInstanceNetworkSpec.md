# ModifyInstanceNetworkSpec {#doc_api_999428 .reference}

修改实例的带宽配置。当实例现有网络规格不满足要求时，可以通过修改实例的带宽配置提高网络性能。

## 描述 {#description .section}

调用该接口时，您需要注意：

-   修改包年包月（PrePaid）实例的带宽配置时：
    -   可以升级或者降配计费方式为按使用流量（PayByTraffic）的带宽。 只能升级计费方式为按固定带宽（PayByBandwidth）的带宽。
    -   公网出带宽（InternetMaxBandwidthOut）从0 Mbps升级到一个非零值时会自动分配一个公网 IP。
    -   您可以通过该接口将带宽计费方式按使用流量（PayByTraffic）转换为按固定带宽（PayByBandwidth）。您只能通过 [ECS管理控制台](https://ecs.console.aliyun.com) 将带宽计费方式按固定带宽（PayByBandwidth）转换为按使用流量（PayByTraffic）。
-   修改按量付费（PostPaid）实例的带宽配置时：
    -   可以升级或者降配带宽。
    -   公网出带宽（InternetMaxBandwidthOut）从0 Mbps升级到一个非零值时会自动分配一个公网 IP。您需要调用 [AllocatePublicIpAddress](~~25544~~) 为实例分配公网IP。
    -   支持将带宽计费方式按使用流量（PayByTraffic）转换为按固定带宽（PayByBandwidth）。
    -   支持将带宽计费方式按固定带宽（PayByBandwidth）转换为按使用流量（PayByTraffic）。
-   对于经典网络（Classic）类型实例，当公网出带宽（InternetMaxBandwidthOut）从0 Mbps升级到一个非零值时，实例必须处于已停止（Stopped）状态。
-   升级带宽后，默认自动扣费。您需要确保账户余额充足，否则会生成异常订单，此时只能作废订单。如果您的账户余额不足，可以将参数AutoPay置为false，此时会生成正常的未支付订单，您可以登录 [ECS管理控制台](https://ecs.console.aliyun.com) 支付。
-   每台预付费（包年包月）实例降低公网带宽的次数不能超过三次，即价格差退款不会超过三次。
-   修改带宽配置前后的价格差退款会退还到您的原付费方式中，已使用的代金券不退回。
-   单个实例每成功操作一次，五分钟内不能继续操作。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyInstanceNetworkSpec)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-xxxxx1|需要修改网络配置的实例ID。

 |
|Action|String|否|ModifyInstanceNetworkSpec|系统规定参数。取值：ModifyInstanceNetworkSpec

 |
|AllocatePublicIp|Boolean|否|false|是否分配公网 IP 地址。默认值：false

 |
|AutoPay|Boolean|否|true|是否自动支付。取值范围：

 -   true：变更带宽配置后，自动扣费。当您将参数 Autopay 置为 true 时，您需要确保账户余额充足，如果账户余额不足会生成异常订单，此订单暂时不支持通过ECS控制台支付，只能作废。
-   false：变更带宽配置后，只生成订单不扣费。如果您的账户余额不足，可以将参数 Autopay 置为 false，即取消自动支付，此时调用该接口会生成正常的未支付订单，此订单可登录 [ECS管理控制台](https://ecs.console.aliyun.com) 支付。

 默认值：true

 |
|ClientToken|String|否|123e4567-e89b-12d3-a456-426655440000|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅 [如何保证幂等性](~~25693~~)。

 |
|EndTime|String|否|2017-12-06T22:40:00Z|临时带宽升级结束时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|InternetMaxBandwidthIn|Integer|否|10|设置公网入带宽最大值，单位：Mbps（Megabit per second）。取值范围：1~200

 |
|InternetMaxBandwidthOut|Integer|否|10|公网出带宽最大值，单位：Mbps（Megabit per second）。取值范围：0~100

 |
|NetworkChargeType|String|否|PayByTraffic|转换网络计费方式。取值范围：

 -   PayByTraffic：按使用流量计费
-   PayByBandwidth：按固定带宽计费

 |
|OwnerAccount|String|否|ECSforCloud@Alibaba.com|RAM 用户的账号登录名称。

 |
|StartTime|String|否|2017-12-05T22:40:00Z|临时带宽升级开始时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|OrderId|String|1111111111111111111111110|生成的订单ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ModifyInstanceNetworkSpec
&RegionId=cn-hangzhou
&InstanceId=i-xxxxx1
&InternetMaxBandwidthOut=10
&ClientToken=xxxxxxxxxxxxxx
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ModifyInstanceNetworkSpecResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyInstanceNetworkSpecResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidInternetMaxBandwidthIn.ValueNotSupported|The specified InternetMaxBandwidthIn is beyond the permitted range.|指定的公网入方向最大带宽超出允许值。|
|400|InvalidInternetMaxBandwidthOut.ValueNotSupported|The specified InternetMaxBandwidthOut is beyond the permitted range.|指定的公网出方向最大带宽超出允许值。|
|403|IncorrectInstanceStatus|The current status of the instance does not support this operation.|当前实例状态不支持此操作。|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|包年包月实例已过期，请您续费后再进行操作。|
|403|ChargeTypeViolation|The operation is not permitted due to billing method of the instance.|实例的计费方式不支持该操作。|
|403|OperationDenied|The operation is denied due to the instance is PrePaid.|实例的计费方式不支持该操作。|
|400|OperationDenied|Specified instance is in VPC.|指定实例存在于 VPC。|
|400|InvalidParameter.Bandwidth|%s|参数不支持。|
|400|InvalidParameter.Conflict|%s|参数冲突。|
|400|Account.Arrearage|Your account has an outstanding payment.|账号存在未支付款项。|
|400|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is invalid.|指定的公网带宽计费方式无效。|
|400|BandwidthUpgradeDenied.EipBoundInstance|The specified VPC instance has bound EIP, temporary bandwidth upgrade is denied.|该实例已经绑定EIP，不能进行临时升级。|
|403|InvalidAccountStatus.NotEnoughBalance|Your account does not have enough balance.|账号余额不足，请您先充值再进行该操作。|
|403|InvalidInstance.UnPaidOrder|The specified Instance has unpaid order.|指定的实例有未支付的订单，请您先支付再进行操作。|
|400|Throttling|Request was denied due to request throttling, please try again after 5 minutes.|请求被流控。|
|400|IpAllocationError|Allocate public ip failed.|公网IP地址分配失败。|
|400|InvalidParam.AllocatePublicIp|The specified param AllocatePublicIp is invalid.|指定的AllocatePublicIp无效。|
|400|InstanceDowngrade.QuotaExceed|Quota of instance downgrade is exceed.|该实例降配已达到最大允许次数。|
|403|InvalidInstance.InstanceNotSupported|The special vpc instance with eip not need bandwidth.|VPC类型实例绑定EIP后不需要指定公网带宽。|
|400|InvalidInstanceStatus|The specified instance status does not support this action.|实例的当前状态不支持该操作。|
|403|InvalidInstanceStatus|The current status of the instance does not support this operation.|实例当前状态不支持该操作。|
|400|InvalidInstance.UnPaidOrder|Unpaid order exists in your account, please complete or cancel the payment in the expense center.|您的账号里有未支付的订单。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

