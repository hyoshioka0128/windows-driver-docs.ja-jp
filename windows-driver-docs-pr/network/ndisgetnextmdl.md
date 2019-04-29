---
title: NdisGetNextMdl macro
description: NdisGetNextMdl マクロでは、現在 MDL へのポインターを受け取り、MDL チェーン内で、[次へ] の MDL を取得します。
ms.assetid: 5b59ca7c-0998-4d53-9553-4946ef85327c
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NdisGetNextMdl マクロ
ms.localizationpriority: medium
ms.openlocfilehash: b65a4d70a345d23531a25ebbec563ed442912add
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338448"
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

**NdisGetNextMdl**マクロの MDL ベースのバージョンの提供、 [ **NdisGetNextBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff552070)関数。

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


[**NdisGetNextBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff552070)

 

 




