---
title: EFI_USBFN_IO_PROTOCOL.FreeTransferBuffer
description: EFI_USBFN_IO_PROTOCOL.FreeTransferBuffer
ms.assetid: 236b925f-2c7b-4df8-b5c8-e8c2f7b853d2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 659ae6f83a21fdf93d1e364b51d1ff7e9e74b4ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573149"
---
# <a name="efiusbfnioprotocolfreetransferbuffer"></a>EFI\_USBFN\_IO\_プロトコル。FreeTransferBuffer


**FreeTransferBuffer**関数によって転送バッファーに割り当てられたメモリの割り当てが解除、 [EFI\_USBFN\_IO\_プロトコル。AllocateTransferBuffer](efi-usbfn-io-protocolallocatetransferbuffer.md)関数。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_FREE_TRANSFER_BUFFER) (
  IN EFI_USBFN_IO_PROTOCOL    *This,
  IN VOID                     *Buffer
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス

<a href="" id="buffer"></a>*バッファー*  
転送バッファーの割り当てを解除へのポインター。

## <a name="return-values"></a>戻り値


この関数は、次の値を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EFI_SUCCESS</strong></p></td>
<td><p>正常に返される関数</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_INVALID_PARAMETER</strong></p></td>
<td><p>パラメーターが無効です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>コメント


## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




