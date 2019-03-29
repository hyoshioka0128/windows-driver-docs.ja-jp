---
title: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpoints
description: EFI_USBFN_IO_PROTOCOL.ConfigureEnableEndpoints
ms.assetid: 31bc58a0-ec2b-4b5e-ad1b-e6107cc083b1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09a3678c88ad507b5e9fbd03533e923beb3f38fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578842"
---
# <a name="efiusbfnioprotocolconfigureenableendpoints"></a>EFI\_USBFN\_IO\_プロトコル。ConfigureEnableEndpoints


**ConfigureEnableEndpoints**関数が指定されたデバイスと構成記述子に基づいてエンドポイントを初期化します。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS) (
  IN EFI_USBFN_IO_PROTOCOL         *This,
  IN EFI_USB_DEVICE_INFO           *DeviceInfo
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="deviceinfo"></a>*DeviceInfo*  
ポインター、 [EFI\_USB\_デバイス\_情報](efi-usb-device-info.md)構造体。

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
<tr class="odd">
<td><p><strong>EFI_OUT_OF_RESOURCES</strong></p></td>
<td><p>リソースの不足が原因、要求を完了できませんでした。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>コメント


この関数が、指定されたを使用してエンドポイントを構成して、ハードウェアは既に初期化されていると仮定*DeviceInfo*ポートをアクティブにし、USB イベントの受信を開始します。

この関数を無視する必要があります、 *bMaxPacketSize0*標準デバイス記述子フィールドと*wMaxPacketSize*指定を介して公開されている標準のエンドポイント記述子フィールド*DeviceInfo*します。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




