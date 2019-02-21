---
title: EFI_USBFN_IO_PROTOCOL します。ConfigureEnableEndpointsEx
description: EFI_USBFN_IO_PROTOCOL します。ConfigureEnableEndpointsEx
ms.assetid: 54DE0D7F-788F-49C3-AF5C-7EDAA0D09D20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0ecd4fac8636e67f6e2e35b9b10071a658cd45c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558331"
---
# <a name="efiusbfnioprotocolconfigureenableendpointsex"></a>EFI\_USBFN\_IO\_プロトコル。ConfigureEnableEndpointsEx


指定されたデバイスと構成の記述子のリストに基づくエンドポイントを構成します。 代替クラス ドライバーがこのメソッドを呼び出すことができます[EFI\_USBFN\_IO\_プロトコル。ConfigureEnableEndpoints](efi-usbfn-io-protocolconfigureenableendpoints.md)します。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS_EX) (
  IN EFI_USBFN_IO_PROTOCOL           *This,
  IN EFI_USB_DEVICE_INFO             *DeviceInfo,
  IN EFI_USB_SUPERSPEED_DEVICE_INFO  *SSDeviceInfo
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="deviceinfo"></a>*DeviceInfo*  
ポインター、 [EFI\_USB\_デバイス\_情報](efi-usb-device-info.md)構造体。

<a href="" id="ssdeviceinfo"></a>*SSDeviceInfo*  
ポインター、 [EFI\_USB\_SUPERSPEED\_デバイス\_情報](efi-usb-superspeed-device-info.md)構造体。

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
<td><p><strong>EFI_UNSUPPORTED</strong></p></td>
<td><p>この操作がサポートされていません。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


この関数は、以降のリビジョン 0x00010002 で利用可能、 **EFI\_USBFN\_IO\_プロトコル**します。

この関数が、指定されたを使用してエンドポイントを構成して、ハードウェアは既に初期化されていると仮定*DeviceInfo*ポートをアクティブにし、USB イベントの受信を開始します。 この関数は*DeviceInfo*と*SSDeviceInfo*オブジェクトし、基になるハードウェアで許可されている最高の速度をサポートするオブジェクトから情報を使用するエンドポイントを構成します。 超高速、高速*DeviceInfo*で渡されたオブジェクトが EFI で同じ DeviceClass 必要\_USB\_デバイス\_記述子。 この関数は EFI を返しますそれ以外の場合、\_サポートされていません。

この関数を無視する必要があります、 *bMaxPacketSize0*標準デバイス記述子フィールドと*wMaxPacketSize*指定を介して公開されている標準のエンドポイント記述子フィールド*DeviceInfo*します。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




