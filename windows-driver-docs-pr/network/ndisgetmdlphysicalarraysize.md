---
title: NdisGetMdlPhysicalArraySize マクロ
description: NdisGetMdlPhysicalArraySize マクロでは、MDL に関連付けられている物理メモリの切断されたブロックの数を取得します。
ms.assetid: 25e3f9a3-3057-4081-af74-427102197906
ms.date: 07/18/2017
keywords:
- Windows Vista 以降のドライバーをネットワーク NdisGetMdlPhysicalArraySize マクロ
ms.localizationpriority: medium
ms.openlocfilehash: 0c6e427eeb78bf24664ddd1669bc4f0308697b8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383681"
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

**NdisGetMdlPhysicalArraySize**マクロの MDL ベースのバージョンの提供、 [ **NdisGetBufferPhysicalArraySize** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552033(v=vs.85))関数。

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
<td><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td><p>DDI 準拠の規則</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-irql-netbuffer-function" data-raw-source="[&lt;strong&gt;Irql_NetBuffer_Function&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-irql-netbuffer-function)"><strong>Irql_NetBuffer_Function</strong></a></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NdisGetBufferPhysicalArraySize**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552033(v=vs.85))

 

 




