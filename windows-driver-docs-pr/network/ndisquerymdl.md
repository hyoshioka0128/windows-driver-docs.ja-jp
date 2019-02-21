---
title: NdisQueryMdl macro
description: NdisQueryMdl マクロは、MDL からバッファー長、および必要に応じてベースの仮想アドレスを取得します。
ms.assetid: 0eccd784-c815-4094-87e5-a3e283abed73
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NdisQueryMdl マクロ
ms.localizationpriority: medium
ms.openlocfilehash: 5003880b56cfb2e96bf18d41b7b2e55c2209ae00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553835"
---
# <a name="ndisquerymdl-macro"></a>NdisQueryMdl macro


**NdisQueryMdl**マクロ MDL からバッファーの長さ、および必要に応じてベースの仮想アドレスを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID NdisQueryMdl(
    _Mdl,
    _VirtualAddress,
    _Length,
    _Priority
);
```

<a name="parameters"></a>パラメーター
----------

*\_Mdl*   
MDL へのポインター。

*\_virtualAddress*   
これでは、このマクロは MDL で説明されている仮想アドレスの範囲の基本の仮想アドレスを返します。 呼び出し元が指定の変数へのポインター。 基本の仮想アドレスは、 **NULL**は次の理由のいずれかの。

-   システム リソースが少ないか容量不足、 *\_優先度*にパラメーターが設定されている**LowPagePriority**または**NormalPagePriority**します。

-   システム リソースが使い果たされると、 *\_優先度*にパラメーターが設定されている**HighPagePriority**します。

*\_長さ*   
このマクロが MDL で説明されている仮想アドレスの範囲のバイト単位の長さを返します、呼び出し元が指定した変数へのポインター。

*\_優先順位*   
ページの優先度値。 このパラメーターに指定できる値の一覧を参照してください、*優先度*のパラメーター、 [ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)マクロ。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**NdisQueryMdl**マクロの MDL ベースのバージョンの提供、 [ **NdisQueryBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff554407)関数。

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


[**MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)

[**NdisQueryBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff554407)

 

 




