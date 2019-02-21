---
title: SM\_AddPort 関数
description: SM\_AddPort WMI メソッドを WMI クライアントに指定されたポートに関連付けられているイベントを通知するために、WMI プロバイダーを構成します。
ms.assetid: 1667487e-80b1-47eb-9f3c-2f5e1909c73b
keywords:
- 記憶装置の SM_AddPort 関数
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
ms.openlocfilehash: 5345d7a40711ec47159fd610796458b7c68447be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560357"
---
# <a name="smaddport-function"></a>SM\_AddPort 関数


SM\_AddPort WMI メソッドを WMI クライアントに指定されたポートに関連付けられているイベントを通知するために、WMI プロバイダーを構成します。

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
られるイベントが報告されますが、ポートを示すワールドワイド名 (WWN)。

*イベントの種類*   
イベントの種類。 このメンバーに割り当てることができる値は、イベントによって定義されます\_型\_修飾子の WMI クラスの修飾子。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_AddPort\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_EventControl WMI クラスです。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SM\_AddPort\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566213)

[**SM\_AddPort\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566215)

 

 






