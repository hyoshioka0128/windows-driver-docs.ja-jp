---
title: EFI_USBFN_IO_PROTOCOL.GetEndpointStallState
description: EFI_USBFN_IO_PROTOCOL.GetEndpointStallState
ms.assetid: abf53ee7-8460-4861-a82d-827ad1dc6c40
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6fde5a4b46ca52fb6f41725974508377ab830d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573082"
---
# <a name="efiusbfnioprotocolgetendpointstallstate"></a>EFI\_USBFN\_IO\_プロトコル。GetEndpointStallState


**GetEndpointStallState**関数は、指定のエンドポイントで停止の状態を返します。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_ENDPOINT_STALL_STATE) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction,
  IN OUT BOOLEAN                  *State
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="endpointindex"></a>*EndpointIndex*  
エンドポイントを示します。

<a href="" id="direction"></a>*方向*  
エンドポイントの方向です。 詳細については、[EFI\_USBFN\_エンドポイント\_方向](efi-usbfn-endpoint-direction.md)を参照してください。

<a href="" id="state"></a>*状態*  
ブール値。**TRUE**値では、停止した状態で、エンドポイントがあることを示します**FALSE**それ以外の場合。

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
</tbody>
</table>

 

## <a name="remarks"></a>コメント


この関数は、 **EFI\_無効な\_パラメーター**指定した方向がエンドポイントの正しくない場合。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




