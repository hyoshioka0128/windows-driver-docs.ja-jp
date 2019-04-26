---
title: EFI_USBFN_IO_PROTOCOL.GetDeviceInfo
description: EFI_USBFN_IO_PROTOCOL.GetDeviceInfo
ms.assetid: b72f6ba1-7704-4661-8855-1ff88bd08e5a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92f35031fd4bec7d933003aef775c01f9d0ae061
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337703"
---
# <a name="efiusbfnioprotocolgetdeviceinfo"></a>EFI\_USBFN\_IO\_プロトコル。GetDeviceInfo


**GetDeviceInfo**関数は、提供された識別子に基づくデバイスに固有の情報を返します。

指定する**EfiUsbDeviceInfoUnknown**ように Id が無効なパラメーターとして扱われます。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_DEVICE_INFO) (
  IN EFI_USBFN_IO_PROTOCOL      *This,
  IN EFI_USBFN_DEVICE_INFO_ID   Id,
  IN OUT UINTN                  *BufferSize,
  OUT VOID                      *Buffer OPTIONAL
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="id"></a>*id*  
A [EFI\_USBFN\_デバイス\_情報\_ID](efi-usbfn-device-info-id.md)要求されたデバイス ID を含む列挙型

<a href="" id="buffersize"></a>*BufferSize*  
入力バッファーのバイト単位のサイズ。 出力では、データの量がバッファーに返されます (バイト単位)。

<a href="" id="buffer"></a>*バッファー*  
Unicode 文字列として、要求された情報が返されるバッファーへのポインター。

## <a name="return-values"></a>戻り値


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
<tr class="odd">
<td><p><strong>EFI_BUFFER_TOO_SMALL</strong></p></td>
<td><p>指定されたバッファーは、要求文字列を保持するのに十分な大きさはありません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


メソッドは、指定されたバッファーが小さすぎるか、NULL の場合は、 **EFI\_バッファー\_すぎます\_小さな**を通して必要なサイズが返される**BufferSize**します。 すべての返される文字列は Unicode 形式です。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




