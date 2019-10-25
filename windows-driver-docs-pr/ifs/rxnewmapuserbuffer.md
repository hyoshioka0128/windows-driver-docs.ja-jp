---
title: RxNewMapUserBuffer 関数
description: RxNewMapUserBuffer は、低 i/o に使用されるユーザーバッファーアドレスを返します。
ms.assetid: 90ab7793-55ed-47f7-b55d-f4205488796c
keywords:
- RxNewMapUserBuffer 関数のインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: a3e98730bf8888210995c9fc5bedd6b1bb45bd9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840974"
---
# <a name="rxnewmapuserbuffer-function"></a>RxNewMapUserBuffer 関数


**RxNewMapUserBuffer**は、低 i/o に使用されるユーザーバッファーアドレスを返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
PVOID RxNewMapUserBuffer(
  _In_ PRX_CONTEXT RxContext
);
```

<a name="parameters"></a>パラメーター
----------

\] の*RxContext* \[  
この要求の RX\_コンテキスト構造体へのポインター。

<a name="return-value"></a>戻り値
------------

**RxNewMapUserBuffer**は、成功した場合はマップされたアドレスポインターを返し、失敗した場合は**NULL**を返します。

<a name="remarks"></a>注釈
-------

MDL が存在する場合は、MDL によってユーザーバッファーが記述され、MDL のシステムアドレスが**RxNewMapUserBuffer**によって返されることが前提となります。 それ以外の場合は、ユーザーバッファーは**RxNewMapUserBuffer**によって直接返されます。

RxNewMapUserBuffer ルーチンは、 *RxContext*変数のの&gt;**Mdladdress**メンバーが**NULL**で**ある-か**どうかを確認**し、** **UserBuffer を&gt;-返します。** この場合の*RxContext*変数のメンバー。 -&gt;**Mdladdress**メンバーが**NULL**でない**場合、** **RxNewMapUserBuffer**は IRP から MDL を返すために[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出します。

**RxNewMapUserBuffer**ルーチンは、windows XP と windows 2000 でのみ使用できます。

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
<td align="left"><p>RxNewMapUserBuffer ルーチンは、Windows XP および Windows 2000 でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Rxprocs (Rxcontx または Rxprocs を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)

[**RxLowIoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiocompletion)

[**RxLowIoGetBufferAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/lowio/nf-lowio-rxlowiogetbufferaddress)

[**RxMapSystemBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxmapsystembuffer)

[**RX\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxcontx/ns-rxcontx-_rx_context)

 

 






