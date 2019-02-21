---
title: NdisQueryMdlOffset macro
description: NdisQueryMdlOffset マクロで物理的なページ内のオフセットを取得する特定の MDL バッファーを開始して、バッファーの長さ。
ms.assetid: d6f23e9c-5015-4087-b7a2-badee00bdafa
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NdisQueryMdlOffset マクロ
ms.localizationpriority: medium
ms.openlocfilehash: ac4ab915d2d096f3262904bb98d8256542aedfe6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552251"
---
# <a name="ndisquerymdloffset-macro"></a>NdisQueryMdlOffset macro


**NdisQueryMdlOffset**マクロで物理的なページ内のオフセットを取得する特定の MDL バッファーを開始して、バッファーの長さ。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID NdisQueryMdlOffset(
    _Mdl,
    _Offset,
    _Length
);
```

<a name="parameters"></a>パラメーター
----------

*\_Mdl*   
MDL へのポインター。

*\_オフセット*   
これでは、このマクロは MDL が指定したバッファーを含む物理ページ内の 0 から始まるバイト オフセットを返します。 呼び出し元が指定の変数へのポインター。

*\_長さ*   
このマクロが MDL で指定されている仮想アドレスの範囲のバイト単位の長さを返します、呼び出し元が指定した変数へのポインター。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**NdisQueryMdlOffset**マクロの MDL ベースのバージョンの提供、 [ **NdisQueryBufferOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff554411)関数。

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
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 準拠の規則</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff547985" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547985)"><strong>Irql_NetBuffer_Function</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisQueryBufferOffset**](https://msdn.microsoft.com/library/windows/hardware/ff554411)

 

 




