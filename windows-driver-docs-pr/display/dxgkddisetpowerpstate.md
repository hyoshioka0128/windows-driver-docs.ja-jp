---
title: DXGKDDISETPOWERPSTATE コールバック関数
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 58DB4615-BD52-4003-8D60-0881E87C7BD3
keywords:
- DxgkDdiSetPowerPState コールバック関数のディスプレイ デバイス
- DXGKDDISETPOWERPSTATE
topic_type:
- apiref
api_name:
- DxgkDdiSetPowerPState
api_location:
- D3dkmddi.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 92559d4af52b9fada84e09620f4ddfda49c6670b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570861"
---
# <a name="dxgkddisetpowerpstate-callback-function"></a>DXGKDDISETPOWERPSTATE コールバック関数


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DXGKDDISETPOWERPSTATE DxgkDdiSetPowerPState;

NTSTATUS APIENTRY DxgkDdiSetPowerPState(
  _In_ const HANDLE DriverContext,
  _In_       UINT   ComponentIndex,
  _In_       UINT   RequestedComponentPState
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*DriverContext* \[で\]

*ComponentIndex* \[in\]

*RequestedComponentPState* \[in\]

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
<td align="left">D3dkmddi.h</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





