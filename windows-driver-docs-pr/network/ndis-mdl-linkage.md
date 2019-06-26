---
title: NDIS_MDL_LINKAGE マクロ
description: NDIS_MDL_LINKAGE マクロでは、指定した MDL に関連付けられている次の MDL へのポインターを取得します。
ms.assetid: 3d5a91cb-cb26-49fb-b510-75fc95f7f46b
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NDIS_MDL_LINKAGE マクロ
ms.localizationpriority: medium
ms.openlocfilehash: 58f91c90d0927c9780d4dde8c742b7d936987bd0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385748"
---
# <a name="ndismdllinkage-macro"></a>NDIS\_MDL\_リンケージ マクロ


**NDIS\_MDL\_リンケージ**マクロを指定した MDL に関連付けられている次の MDL へのポインターを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PVOID NDIS_MDL_LINKAGE(
   PMDL _Mdl
);
```

<a name="parameters"></a>パラメーター
----------

*\_Mdl*   
MDL へのポインター。

<a name="return-value"></a>戻り値
------------

**NDIS\_MDL\_リンケージ**MDL へのポインターを返しますまたは**NULL**次 MDL がない場合。

<a name="remarks"></a>注釈
-------

**NDIS\_MDL\_リンケージ**マクロの MDL ベースのバージョンの提供、 [ **NDIS\_バッファー\_リンケージ**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556919(v=vs.85))関数。

<a name="requirements"></a>要件
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


[**NDIS\_バッファー\_リンケージ**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff556919(v=vs.85))

 

 




