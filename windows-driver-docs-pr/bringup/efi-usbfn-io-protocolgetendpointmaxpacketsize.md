---
title: EFI_USBFN_IO_PROTOCOL します。GetEndpointMaxPacketSize
description: EFI_USBFN_IO_PROTOCOL します。GetEndpointMaxPacketSize
ms.assetid: 0af72372-7c58-490d-8eec-bd38bce09b0d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0571eb866c0566b0e82ca390fbfb9ba3b64aed7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549957"
---
# <a name="efiusbfnioprotocolgetendpointmaxpacketsize"></a>EFI\_USBFN\_IO\_プロトコル。GetEndpointMaxPacketSize


**GetEndpointMaxPacketSize**関数は、指定したバス速度の指定したエンドポイントの種類のパケットの最大サイズを返します.

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_GET_ENDPOINT_MAXPACKET_SIZE) (
  IN EFI_USBFN_IO_PROTOCOL      *This,
  IN EFI_USB_ENDPOINT_TYPE      EndpointType,
  IN EFI_USB_BUS_SPEED          BusSpeed,
  OUT UINT16                    *MaxPacketSize
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="endpointtype"></a>*EndpointType*  
エンドポイントの種類で定義されている、 [EFI\_USB\_エンドポイント\_型](efi-usb-endpoint-type.md)します。 列挙

<a href="" id="busspeed"></a>*BusSpeed*  
[EFI\_USB\_BUS\_速度](efi-usb-bus-speed.md)既知の呼び出し元に現在のバス速度を示す列挙値。

<a href="" id="maxpacketsize"></a>*この*  
指定したエンドポイントの種類のバイト単位の最大パケット サイズ。

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

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




