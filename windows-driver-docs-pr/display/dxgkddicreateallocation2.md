---
title: DXGKDDI\_CREATEALLOCATION2 コールバック関数
description: DxgkDdiCreateAllocation2 関数は、システムの使用に予約されています。 ドライバーは、実装されていません。
ms.assetid: c22e176e-cde5-4edf-8f53-1d7874c7d5da
keywords:
- DxgkDdiCreateAllocation2 コールバック関数のディスプレイ デバイス
- DXGKDDI_CREATEALLOCATION2
topic_type:
- apiref
api_name:
- DxgkDdiCreateAllocation2
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: dfcd61d26e5d7bd0730acc3fc717120a833c83e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331297"
---
# <a name="dxgkddicreateallocation2-callback-function"></a>DXGKDDI\_CREATEALLOCATION2 コールバック関数


\[システムの使用に予約されています。\]

*DxgkDdiCreateAllocation2*関数はシステム用に予約されています。 ドライバーは、実装されていません。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DXGKDDI_CREATEALLOCATION2 DxgkDdiCreateAllocation2;

NTSTATUS DxgkDdiCreateAllocation2(
   IN_CONST_HANDLE                  hAdapter,
   INOUT_PDXGKARG_CREATEALLOCATION2 pCreateAllocation
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*hAdapter*システム使用するためにこのパラメーターは予約されています。

*pCreateAllocation*システム使用するためにこのパラメーターは予約されています。

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
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h (D3dkmddi.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





