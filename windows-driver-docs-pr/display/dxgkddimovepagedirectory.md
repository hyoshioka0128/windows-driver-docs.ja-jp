---
title: DxgkDdiMovePageDirectory 関数
description: DxgkDdiMovePageDirectory 関数は、システムの使用に予約されています。 ドライバーは、実装されていません。
ms.assetid: 25972570-174d-40dc-bfbc-e9eb395dcb0e
keywords:
- ディスプレイ デバイスの DxgkDdiMovePageDirectory 関数
topic_type:
- apiref
api_name:
- DxgkDdiMovePageDirectory
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f326ad39f877af4d363f92373a38fdcbaacc5a0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552544"
---
# <a name="dxgkddimovepagedirectory-function"></a>DxgkDdiMovePageDirectory 関数


\[システムの使用に予約されています。\]

*DxgkDdiMovePageDirectory*関数はシステム用に予約されています。 ドライバーは、実装されていません。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
NTSTATUS APIENTRY DxgkDdiMovePageDirectory(
  _In_    CONST HANDLE              hContext,
  _Inout_ DXGKARG_MOVEPAGEDIRECTORY *pMovePageDirectory
);
```

<a name="parameters"></a>パラメーター
----------

*hContext* \[で\]システム使用するためにこのパラメーターは予約されています。

*pMovePageDirectory* \[入力、出力\]システム使用するためにこのパラメーターは予約されています。

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

 

 





