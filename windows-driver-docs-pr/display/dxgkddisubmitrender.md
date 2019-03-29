---
title: DXGKDDI\_SUBMITRENDER コールバック関数
description: DxgkDdiSubmitRender 関数は、システムの使用に予約されています。 ドライバーは、実装されていません。
ms.assetid: a409f737-72e9-43b0-be81-c373b151f5d9
keywords:
- DxgkDdiSubmitRender コールバック関数のディスプレイ デバイス
- DXGKDDI_SUBMITRENDER
topic_type:
- apiref
api_name:
- DxgkDdiSubmitRender
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 494a0289335c5484008a94ec88884fcf9dcbddfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579898"
---
# <a name="dxgkddisubmitrender-callback-function"></a>DXGKDDI\_SUBMITRENDER コールバック関数


\[システムの使用に予約されています。\]

*DxgkDdiSubmitRender*関数はシステム用に予約されています。 ドライバーは、実装されていません。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DXGKDDI_SUBMITRENDER DxgkDdiSubmitRender;

NTSTATUS DxgkDdiSubmitRender(
   IN_CONST_HANDLE             hContext,
   INOUT_PDXGKARG_SUBMITRENDER pSubmitRender
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*hContext*システム使用するためにこのパラメーターは予約されています。

*pSubmitRender*システム使用するためにこのパラメーターは予約されています。

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
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





