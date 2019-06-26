---
title: RxNewMapUserBuffer 関数
description: RxNewMapUserBuffer 低い I/O で使用されるユーザー バッファーのアドレスを返します。
ms.assetid: 90ab7793-55ed-47f7-b55d-f4205488796c
keywords:
- インストール可能なファイル システム ドライバーの RxNewMapUserBuffer 関数
topic_type:
- apiref
api_name:
- RxNewMapUserBuffer
api_location:
- rxprocs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1eed833830e1ba889ac011875314cf14dab6ccdc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359266"
---
# <a name="rxnewmapuserbuffer-function"></a>RxNewMapUserBuffer 関数


**RxNewMapUserBuffer**低い I/O で使用されるユーザー バッファーのアドレスを返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PVOID RxNewMapUserBuffer(
  _In_ PRX_CONTEXT RxContext
);
```

<a name="parameters"></a>パラメーター
----------

*RxContext* \[in\]  
RX へのポインター\_この要求のコンテキスト構造体。

<a name="return-value"></a>戻り値
------------

**RxNewMapUserBuffer**成功した場合にマップされたアドレスのポインターを返しますまたは**NULL**失敗します。

<a name="remarks"></a>注釈
-------

MDL が存在するかどうかは、MDL バッファーを記述、ユーザー、および、MDL のシステム アドレスは、によって返されることが前提です**RxNewMapUserBuffer**します。 それ以外の場合、ユーザー バッファーがによって直接返される**RxNewMapUserBuffer**します。

**RxNewMapUserBuffer**ルーチン チェックの場合、 **CurrentIrp**-&gt;**MdlAddress**のメンバー、 *RxContext*変数**NULL**を返します、 **CurrentIrp**-&gt;**UserBuffer**のメンバー、 *RxContext*変数とこれに該当します。 場合、 **CurrentIrp**-&gt;**MdlAddress**メンバーでない**NULL**、し**RxNewMapUserBuffer**されます呼び出す[ **MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) IRP から MDL を返す。

なお、 **RxNewMapUserBuffer**ルーチンは Windows XP および Windows 2000 で利用できるのみです。

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
<td align="left"><p>RxNewMapUserBuffer ルーチンは、Windows XP および Windows 2000 にできるだけです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Rxprocs.h (Rxcontx.h または Rxprocs.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**RxLowIoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiocompletion)

[**RxLowIoGetBufferAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/lowio/nf-lowio-rxlowiogetbufferaddress)

[**RxMapSystemBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxmapsystembuffer)

[**RX\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxcontx/ns-rxcontx-_rx_context)

 

 






