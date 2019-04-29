---
title: DXGKDDI\_UPDATEPAGETABLE コールバック関数
description: DxgkDdiUpdatePageTable 関数は、システムの使用に予約されています。 ドライバーは、実装されていません。
ms.assetid: 08328e82-d1cc-4c50-bc96-7382232676ab
keywords:
- DxgkDdiUpdatePageTable コールバック関数のディスプレイ デバイス
- DXGKDDI_UPDATEPAGETABLE
topic_type:
- apiref
api_name:
- DxgkDdiUpdatePageTable
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 332293a5255408a07f1895ec68b316451733652e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323270"
---
# <a name="dxgkddiupdatepagetable-callback-function"></a>DXGKDDI\_UPDATEPAGETABLE コールバック関数


\[システムの使用に予約されています。\]

*DxgkDdiUpdatePageTable*関数はシステム用に予約されています。 ドライバーは、実装されていません。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DXGKDDI_UPDATEPAGETABLE DxgkDdiUpdatePageTable;

NTSTATUS DxgkDdiUpdatePageTable(
   IN_CONST_HANDLE                hDevice,
   INOUT_PDXGKARG_UPDATEPAGETABLE pUpdatePageTable
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*hDevice*システム使用するためにこのパラメーターは予約されています。

*pUpdatePageTable*システム使用するためにこのパラメーターは予約されています。

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
<td align="left">Dispmprt.h</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





