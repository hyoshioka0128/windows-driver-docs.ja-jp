---
title: NdisGetNextMdl macro
description: NdisGetNextMdl マクロでは、現在 MDL へのポインターを受け取り、MDL チェーン内で、[次へ] の MDL を取得します。
ms.assetid: 5b59ca7c-0998-4d53-9553-4946ef85327c
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NdisGetNextMdl マクロ
ms.localizationpriority: medium
ms.openlocfilehash: 1280211dfee544e8c35a2e2823875be824290355
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383677"
---
# <a name="ndisgetnextmdl-macro"></a>NdisGetNextMdl macro


**NdisGetNextMdl**マクロが現在 MDL へのポインターを受け取り、MDL チェーン内で、[次へ] の MDL を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID NdisGetNextMdl(
    _CurrentMdl,
    _NextMdl
);
```

<a name="parameters"></a>パラメーター
----------

*\_CurrentMdl*   
指定された現在 MDL へのポインター。

*\_NextMdl*   
後の存在する場合にこのマクロが、MDL チェーン内で [次へ] MDL のポインターを返しますが、呼び出し元が指定した変数へのポインター、ある MDL  *\_CurrentMdl*します。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**NdisGetNextMdl**マクロの MDL ベースのバージョンの提供、 [ **NdisGetNextBuffer** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552070(v=vs.85))関数。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
<tr class="even">
<td><p>バージョン</p></td>
<td><p>NDIS 6.0 以降をサポートします。</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>任意のレベル</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisGetNextBuffer**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552070(v=vs.85))

 

 




