---
title: DxgkDdiUpdatePageDirectory 関数
description: DxgkDdiUpdatePageDirectory 関数は、システムの使用に予約されています。 ドライバーは、実装されていません。
ms.assetid: 91f81165-a63c-44bb-8898-9cc85c2a6e45
keywords:
- ディスプレイ デバイスの DxgkDdiUpdatePageDirectory 関数
topic_type:
- apiref
api_name:
- DxgkDdiUpdatePageDirectory
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 138ae874d0a1935c65c7d80462537615a0c36244
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553014"
---
# <a name="dxgkddiupdatepagedirectory-function"></a>DxgkDdiUpdatePageDirectory 関数


\[システムの使用に予約されています。\]

*DxgkDdiUpdatePageDirectory*関数はシステム用に予約されています。 ドライバーは、実装されていません。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS APIENTRY DxgkDdiUpdatePageDirectory(
   IN_CONST_HANDLE                    hDevice,
   INOUT_PDXGKARG_UPDATEPAGEDIRECTORY pUpdatePageDirectory
);
```

<a name="parameters"></a>パラメーター
----------

*hDevice*システム使用するためにこのパラメーターは予約されています。

*pUpdatePageDirectory*システム使用するためにこのパラメーターは予約されています。

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
<td align="left">Dispmprt.h (Dispmprt.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

 

 





