---
title: DXGKDDI\_DESCRIBEPAGETABLE コールバック関数
description: DxgkDdiDescribePageTable 関数は、システムの使用に予約されています。 ドライバーは、実装されていません。
ms.assetid: af9c9515-0225-4a97-bb8e-8ff9b57ac1a9
keywords:
- DxgkDdiDescribePageTable コールバック関数のディスプレイ デバイス
- DXGKDDI_DESCRIBEPAGETABLE
topic_type:
- apiref
api_name:
- DxgkDdiDescribePageTable
api_location:
- Dispmprt.h
api_type:
- UserDefined
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 525b353f1b57e0fe06c6c388d6b22d23e20a61ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579899"
---
# <a name="dxgkddidescribepagetable-callback-function"></a>DXGKDDI\_DESCRIBEPAGETABLE コールバック関数


\[システムの使用に予約されています。\]

*DxgkDdiDescribePageTable*関数はシステム用に予約されています。 ドライバーは、実装されていません。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DXGKDDI_DESCRIBEPAGETABLE DxgkDdiDescribePageTable;

NTSTATUS DxgkDdiDescribePageTable(
   IN_CONST_HANDLE                  hDevice,
   INOUT_PDXGKARG_DESCRIBEPAGETABLE pDescribePageTable
)
{ ... }
```

<a name="parameters"></a>パラメーター
----------

*hDevice*システム使用するためにこのパラメーターは予約されています。

*pDescribePageTable*システム使用するためにこのパラメーターは予約されています。

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
<td align="left">Dispmprt.h (Dispmprt.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





