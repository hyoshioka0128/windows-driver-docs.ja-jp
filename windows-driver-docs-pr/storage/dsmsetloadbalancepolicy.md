---
title: DsmSetLoadBalancePolicy 関数
description: DsmSetLoadBalancePolicy メソッドは、DSM の負荷分散ポリシーを設定するために使用されます。
ms.assetid: f53a776a-b350-4424-855a-49323587c57b
keywords:
- DsmSetLoadBalancePolicy function Storage デバイス
topic_type:
- apiref
api_name:
- DsmSetLoadBalancePolicy
api_location:
- MPIOdisk.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c061b110b87b368bf5fbfca16e3d5489f9851049
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844557"
---
# <a name="dsmsetloadbalancepolicy-function"></a>DsmSetLoadBalancePolicy 関数


**DsmSetLoadBalancePolicy**メソッドは、DSM の負荷分散ポリシーを設定するために使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void DsmSetLoadBalancePolicy(
   [in, Description("New Load Balance policy to be set"):amended] DSM_Load_Balance_Policy LoadBalancePolicy,
   [out, Description("Status of the operation"):amended] uint32                           Status
);
```

<a name="parameters"></a>パラメーター
----------

*LoadBalancePolicy*   
[**DsmSetLoadBalancePolicy\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsmsetloadbalancepolicy_out)構造体。

*状態*   
操作の状態。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [DSM\_LB\_Operations](dsm-lb-operations-wmi-class.md) WMI クラスに属しています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">MPIOdisk .h (MPIOdisk. h を含む)</td>
</tr>
</tbody>
</table>

 

 





