---
title: EFI_USBFN_IO_PROTOCOL.GetMaxTransferSize
description: EFI_USBFN_IO_PROTOCOL.GetMaxTransferSize
ms.assetid: 61160708-029b-4691-87fe-22d06424220d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e20d650747a0b14c572c5088c264e014d12e18f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570978"
---
# <a name="efiusbfnioprotocolgetmaxtransfersize"></a>EFI\_USBFN\_IO\_プロトコル。GetMaxTransferSize


**GetMaxTransferSize**関数は、基になる、コント ローラーでサポートされる最大転送サイズを返します。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_MAXTRANSFER_SIZE) (
  IN EFI_USBFN_IO_PROTOCOL     *This,
  OUT UINTN                    *MaxTransferSize
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="maxtransfersize"></a>*MaxTransferSize*  
サポートされている転送の最大サイズ (バイト単位)。

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
<td><p><strong>EFI_DEVICE_ERROR</strong></p></td>
<td><p>物理デバイスには、エラーが報告されました。</p></td>
</tr>
<tr class="even">
<td><p><strong>EFI_NOT_READY</strong></p></td>
<td><p>物理デバイスがビジー状態か、この要求を処理する準備ができていません</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>コメント


## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




