---
title: SM\_AddPort 関数
description: SM\_AddPort WMI メソッドは、指定されたポートに関連付けられているイベントを WMI クライアントに通知するように WMI プロバイダーを構成します。
ms.assetid: 1667487e-80b1-47eb-9f3c-2f5e1909c73b
keywords:
- SM_AddPort 関数記憶装置
topic_type:
- apiref
api_name:
- SM_AddPort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fb25c4d9a97825af5e9d2bbd60e34cb7f5e852c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845491"
---
# <a name="sm_addport-function"></a>SM\_AddPort 関数


SM\_AddPort WMI メソッドは、指定されたポートに関連付けられているイベントを WMI クライアントに通知するように WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_AddPort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [in, EVENT_TYPES_QUALIFIERS] uint32     EventType,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN*   
イベントが報告されるポートを示すワールドワイド名 (WWN)。

*EventType*   
イベントの種類。 このメンバーに割り当てることができる値は、イベント\_の種類\_修飾子 WMI クラス修飾子によって定義されます。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_AddPort\_OUT 構造の HBAStatus メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_EventControl WMI クラスに属しています。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**SM\_AddPort\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addport_in)

[**SM\_AddPort\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_addport_out)

 

 






