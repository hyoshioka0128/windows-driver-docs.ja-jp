---
title: EFI_USBFN_IO_PROTOCOL.SetEndpointStallState
description: EFI_USBFN_IO_PROTOCOL.SetEndpointStallState
ms.assetid: bd754296-5002-48b6-9986-fa09c2094470
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1f2df4b3b5f81bc2e9b78ea27c9b306b83e9f5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337672"
---
# <a name="efiusbfnioprotocolsetendpointstallstate"></a>EFI\_USBFN\_IO\_プロトコル。SetEndpointStallState


**SetEndpointStallState**関数を設定または指定したエンドポイントの停止状態をクリアします。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_SET_ENDPOINT_STALL_STATE) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  IN UINT8                        EndpointIndex,
  IN EFI_USBFN_ENDPOINT_DIRECTION Direction,
  IN BOOLEAN                      State
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="endpointindex"></a>*EndpointIndex*  
エンドポイントを停止している必要があることを示します。

<a href="" id="direction"></a>*方向*  
エンドポイントの方向です。 詳細については、次を参照してください。 [EFI\_USBFN\_エンドポイント\_方向](efi-usbfn-endpoint-direction.md)します。

<a href="" id="state"></a>*状態*  
指定したエンドポイントの停止の状態を要求します。 このパラメーターを設定**TRUE**直さざるを得ないというエンドポイントをによりします。 設定すると**FALSE**既存の停止をクリアします。

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

 

 




