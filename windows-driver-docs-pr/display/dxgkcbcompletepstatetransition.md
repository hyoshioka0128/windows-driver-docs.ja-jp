---
title: DXGKCB\_COMPLETEPSTATETRANSITION コールバック関数
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: F0EF1B1F-58C3-4D6D-BF9A-0621CC82ED6B
keywords:
- DxgkCbCompletePStateTransition コールバック関数のディスプレイ デバイス
- DXGKCB_COMPLETEPSTATETRANSITION
topic_type:
- apiref
api_name:
- DxgkCbCompletePStateTransition
api_location:
- D3dkmddi.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 58b1f3961f8ca78a1fb625b079315dfc23b69b96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341104"
---
# <a name="dxgkcbcompletepstatetransition-callback-function"></a>DXGKCB\_COMPLETEPSTATETRANSITION コールバック関数


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DXGKCB_COMPLETEPSTATETRANSITION DxgkCbCompletePStateTransition;

VOID APIENTRY CALLBACK* DxgkCbCompletePStateTransition(
  _In_ const HANDLE hAdapter,
  _In_       UINT   ComponentIndex,
  _In_       UINT   CompletedPState
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*hAdapter* \[で\]

*ComponentIndex* \[in\]

*CompletedPState* \[in\]

<a name="return-value"></a>戻り値
------------

このコールバック関数では、値は返されません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h (include D3dkmddi.h)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





