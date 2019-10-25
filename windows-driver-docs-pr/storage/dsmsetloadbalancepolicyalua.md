---
title: DsmSetLoadBalancePolicyALUA 関数
description: DsmSetLoadBalancePolicyALUA メソッドは、DSM ALUA の負荷分散ポリシーを設定するために使用されます。
ms.assetid: f63bdf0a-5b78-475d-b7c5-2af587b6356f
keywords:
- DsmSetLoadBalancePolicyALUA function Storage デバイス
topic_type:
- apiref
api_name:
- DsmSetLoadBalancePolicyALUA
api_location:
- MPIOdisk.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f7f75320262701266f584b9851e7344ce723d0a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844559"
---
# <a name="dsmsetloadbalancepolicyalua-function"></a>DsmSetLoadBalancePolicyALUA 関数


**DsmSetLoadBalancePolicyALUA**メソッドは、DSM ALUA の負荷分散ポリシーを設定するために使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void DsmSetLoadBalancePolicyALUA(
   [in, Description("New Load Balance policy to be set"):amended] DSM_Load_Balance_Policy_V2 LoadBalancePolicy,
   [out, Description("Status of the operation"):amended] uint32                              Status
);
```

<a name="parameters"></a>パラメーター
----------

*LoadBalancePolicy*   
[**DsmSetLoadBalancePolicyALUA\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsmsetloadbalancepolicyalua_out)構造体。

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

 

 





