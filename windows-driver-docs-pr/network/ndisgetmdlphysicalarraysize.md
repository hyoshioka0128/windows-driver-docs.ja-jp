---
title: NdisGetMdlPhysicalArraySize マクロ
description: NdisGetMdlPhysicalArraySize マクロでは、MDL に関連付けられている物理メモリの切断されたブロックの数を取得します。
ms.assetid: 25e3f9a3-3057-4081-af74-427102197906
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NdisGetMdlPhysicalArraySize マクロ
ms.localizationpriority: medium
ms.openlocfilehash: bc8cd67880d36826e04479559492b713ab7fa6bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550644"
---
# <a name="ndisgetmdlphysicalarraysize-macro"></a>NdisGetMdlPhysicalArraySize マクロ


**NdisGetMdlPhysicalArraySize**マクロ、MDL に関連付けられている物理メモリが切断されているブロックの数を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID NdisGetMdlPhysicalArraySize(
    _Mdl,
    _ArraySize
);
```

<a name="parameters"></a>パラメーター
----------

*\_Mdl*   
MDL へのポインター。

*\_ArraySize*   
このマクロがの数を返しますが、呼び出し元が指定した変数へのポインターには、指定した MDL に関連付けられている物理メモリのブロックが切断されました。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

**NdisGetMdlPhysicalArraySize**マクロの MDL ベースのバージョンの提供、 [ **NdisGetBufferPhysicalArraySize** ](https://msdn.microsoft.com/library/windows/hardware/ff552033)関数。

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


[**NdisGetBufferPhysicalArraySize**](https://msdn.microsoft.com/library/windows/hardware/ff552033)

 

 




