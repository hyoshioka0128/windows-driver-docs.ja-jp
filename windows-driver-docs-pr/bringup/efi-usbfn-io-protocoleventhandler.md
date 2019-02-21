---
title: EFI_USBFN_IO_PROTOCOL します。イベント ハンドラー
description: EFI_USBFN_IO_PROTOCOL します。イベント ハンドラー
ms.assetid: d493de90-cb8c-44d1-8999-f1ceb26e5c15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff785fedb41a40e0425fbb75465aec14a94368c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558333"
---
# <a name="efiusbfnioprotocoleventhandler"></a>EFI\_USBFN\_IO\_プロトコル。イベント ハンドラー


**EventHandler** USB バス状態の更新プログラムを受信、受信、エンドポイント、状態の変更を送信し、0 のエンドポイントでパケットを設定する関数を繰り返し呼び出されます。

## <a name="syntax"></a>構文


```cpp
typedef
EFI_STATUS
(EFIAPI * EFI_USBFN_IO_EVENTHANDLER) (
  IN EFI_USBFN_IO_PROTOCOL        *This,
  OUT EFI_USBFN_MESSAGE           *Message,
  IN OUT UINTN                    *PayloadSize,
  OUT EFI_USBFN_MESSAGE_PAYLOAD   *Payload
  );
```

## <a name="parameters"></a>パラメーター


<a href="" id="this"></a>*これ*  
EFI へのポインター\_USBFN\_IO\_プロトコル インスタンス。

<a href="" id="message"></a>*メッセージ*  
A [EFI\_USBFN\_メッセージ](efi-usbfn-message.md)この通知を開始したイベントを示す値。

<a href="" id="payloadsize"></a>*PayloadSize*  
入力でメモリのサイズはペイロードを指しています。 出力では、データの量は、ペイロードで返されます。

<a href="" id="payload"></a>*ペイロード*  
ポインター、 [EFI\_USBFN\_メッセージ\_ペイロード](efi-usbfn-message-payload.md)インスタンスを現在のメッセージの追加のペイロードを返します。

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
<td><p>指定されたバッファーがメッセージ ペイロードを保持するために大きくないです。</p></td>
</tr>
</tbody>
</table>

 

## <a name="remarks"></a>注釈


クラスのドライバーでは、さまざまなエンドポイントに転送されたバイト数と転送の状態に更新プログラムを受信するには、繰り返しイベント ハンドラーを呼び出す必要があります。 参照してください[UEFI シーケンス図](uefi-sequence-diagram.md)についてさらにします。

いくつかのメッセージには、指定されたバッファーに返されるペイロードが関連付けられています。 次の表には、さまざまなメッセージとそのペイロードがについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>メッセージ</th>
<th>ペイロード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EfiUsbMsgSetupPacket</p></td>
<td><p>EFI_USB_DEVICE_REQUEST</p></td>
<td><p>セットアップのパケットを受信しました</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgEndpointStatusChangedRx</p></td>
<td><p><a href="efi-usbfn-transfer-result.md" data-raw-source="[EFI_USBFN_TRANSFER_RESULT](efi-usbfn-transfer-result.md)">EFI_USBFN_TRANSFER_RESULT</a></p></td>
<td><p>要求されたデータの一部は、ホストに転送されました。 残りのデータを再送信する必要があるかどうかを判断するクラス ドライバーの役目です。 指定されたバッファー <a href="efi-usbfn-io-protocoltransfer.md" data-raw-source="[EFI_USBFN_IO_PROTOCOL.Transfer](efi-usbfn-io-protocoltransfer.md)">EFI_USBFN_IO_PROTOCOL します。転送</a>r は、ペイロードのバッファー フィールドと同じである必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgEndpointStatusChangedTx</p></td>
<td><p><a href="efi-usbfn-transfer-result.md" data-raw-source="[EFI_USBFN_TRANSFER_RESULT](efi-usbfn-transfer-result.md)">EFI_USBFN_TRANSFER_RESULT</a></p></td>
<td><p>ホストからも、要求されたデータの一部が受け取らします。 残りのデータを待機する必要があるかどうかをクラス ドライバーの役目です。 指定されたバッファー <a href="efi-usbfn-io-protocoltransfer.md" data-raw-source="[EFI_USBFN_IO_PROTOCOL.Transfer](efi-usbfn-io-protocoltransfer.md)">EFI_USBFN_IO_PROTOCOL します。転送</a>ペイロードのバッファー フィールドと同じである必要があります。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventReset</p></td>
<td><p>なし</p></td>
<td><p>リセット バス イベントがシグナル状態にします。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventDetach</p></td>
<td><p>なし</p></td>
<td><p>デタッチ バス イベントがシグナル状態にします。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventAttach</p></td>
<td><p>なし</p></td>
<td><p>アタッチのバスのイベントがシグナル状態にします。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventSuspend</p></td>
<td><p>なし</p></td>
<td><p>中断バス イベントがシグナル状態にします。</p></td>
</tr>
<tr class="even">
<td><p>EfiUsbMsgBusEventResume</p></td>
<td><p>なし</p></td>
<td><p>バス イベントがシグナルを再開します。</p></td>
</tr>
<tr class="odd">
<td><p>EfiUsbMsgBusEventSpeed</p></td>
<td><p><a href="efi-usb-bus-speed.md" data-raw-source="[EFI_USB_BUS_SPEED](efi-usb-bus-speed.md)">EFI_USB_BUS_SPEED</a></p></td>
<td><p>バス速度の更新が通知されます。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




