---
title: DXGKCB\_存在\_と\_進行状況のコールバック関数
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 8970246b-b46f-464f-93b2-973cc351ed07
keywords:
- pfnPresentDisplayOnlyProgress コールバック関数のディスプレイ デバイス
- DXGKCB_PRESENT_DISPLAYONLY_PROGRESS
topic_type:
- apiref
api_name:
- pfnPresentDisplayOnlyProgress
api_location:
- D3dkmddi.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 67306955be711f55f169aa36727f6293e779e39d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570864"
---
# <a name="dxgkcbpresentdisplayonlyprogress-callback-function"></a>DXGKCB\_存在\_と\_進行状況のコールバック関数


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DXGKCB_PRESENT_DISPLAYONLY_PROGRESS pfnPresentDisplayOnlyProgress;

void APIENTRY CALLBACK* pfnPresentDisplayOnlyProgress(
  _In_ const HANDLE                                 hAdapter,
  _In_ const DXGKARGCB_PRESENT_DISPLAYONLY_PROGRESS *pProgress
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*hAdapter* \[で\]

*pProgress* \[in\]

<a name="return-value"></a>戻り値
------------

このコールバック関数では、値は返されません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h</td>
</tr>
</tbody>
</table>

 

 





