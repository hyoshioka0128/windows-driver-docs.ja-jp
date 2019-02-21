---
title: EFI_USBFN_IO_PROTOCOL します。AllocateTransferBuffer
description: EFI_USBFN_IO_PROTOCOL します。AllocateTransferBuffer
ms.assetid: dbaa4f18-97b5-4867-9e03-de19b2253722
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a2123eb4e494cc8b9362d96b34d8c7822e94442
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537827"
---
# <a name="efiusbfnioprotocolallocatetransferbuffer"></a>EFI\_USBFN\_IO\_プロトコル。AllocateTransferBuffer


**AllocateTransferBuffer**関数は、コント ローラーの要件を満たす、指定されたサイズの転送バッファーを割り当てます。

一致する呼び出しに使用して割り当てられた転送バッファーを解放する必要があります、 **FreeTransferBuffer**関数。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_ALLOCATE_TRANSFER_BUFFER) (
  IN EFI_USBFN_IO_PROTOCOL    *This,
  IN UINTN                    Size,
  OUT VOID                    **Buffer
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="size"></a>*サイズ*  
転送バッファーに割り当てるバイト数。

<a href="" id="buffer"></a>*バッファー*  
呼び出しが成功した場合、割り当てられたバッファーへのポインターへのポインターそれ以外の場合に定義されていません。

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
<tr class="odd">
<td><p><strong>EFI_OUT_OF_RESOURCES</strong></p></td>
<td><p>要求された転送バッファーを割り当てられませんでした。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




