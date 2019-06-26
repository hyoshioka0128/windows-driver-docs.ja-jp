---
title: DsmSetLoadBalancePolicy 関数
description: DsmSetLoadBalancePolicy メソッドは、DSM の負荷分散ポリシーの設定に使用されます。
ms.assetid: f53a776a-b350-4424-855a-49323587c57b
keywords:
- 記憶装置の DsmSetLoadBalancePolicy 関数
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
ms.openlocfilehash: e77d64da9d540cdefbe767f92af8041705e45c32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373211"
---
# <a name="dsmsetloadbalancepolicy-function"></a>DsmSetLoadBalancePolicy 関数


**DsmSetLoadBalancePolicy** DSM の負荷分散ポリシーを設定するメソッドを使用します。

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
A [ **DsmSetLoadBalancePolicy\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiodisk/ns-mpiodisk-_dsmsetloadbalancepolicy_out)構造体。

*状態*   
操作の状態。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [DSM\_LB\_操作](dsm-lb-operations-wmi-class.md)WMI クラスです。

<a name="requirements"></a>必要条件
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
<td align="left">MPIOdisk.h (MPIOdisk.h を含む)</td>
</tr>
</tbody>
</table>

 

 





