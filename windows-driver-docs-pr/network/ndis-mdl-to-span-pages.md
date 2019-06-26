---
title: NDIS_MDL_TO_SPAN_PAGES マクロ
description: NDIS_MDL_TO_SPAN_PAGES マクロでは、特定 MDL のバックアップに使用されているメモリの物理ページの数を取得します。
ms.assetid: 8c9df989-4a5f-4ec1-9544-29b59517a502
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NDIS_MDL_TO_SPAN_PAGES マクロ
ms.localizationpriority: medium
ms.openlocfilehash: 4c69272cb175c5dd228f6dd73c4b48944c8a0067
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385743"
---
# <a name="ndismdltospanpages-macro"></a>NDIS\_MDL\_TO\_スパン\_ページ マクロ


**NDIS\_MDL\_TO\_スパン\_ページ**マクロが特定 MDL のバックアップに使用されているメモリの物理ページの数を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
int NDIS_MDL_TO_SPAN_PAGES(
   PMDL _Mdl
);
```

<a name="parameters"></a>パラメーター
----------

*\_Mdl*   
MDL へのポインター。

<a name="return-value"></a>戻り値
------------

**NDIS\_MDL\_TO\_スパン\_ページ**MDL の仮想アドレスの範囲にバックアップするページの数を返します。

<a name="remarks"></a>注釈
-------

**NDIS\_MDL\_TO\_スパン\_ページ**マクロの MDL ベースのバージョンの提供、 [ **NDIS\_バッファー\_TO\_スパン\_ページ**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556922(v=vs.85))関数。

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


[**NDIS\_バッファー\_TO\_スパン\_ページ**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556922(v=vs.85))

 

 




