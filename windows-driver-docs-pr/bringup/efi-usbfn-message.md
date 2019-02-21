---
title: EFI_USBFN_MESSAGE
description: EFI_USBFN_MESSAGE
ms.assetid: 411890e1-8913-4e47-acd5-1b36b1b05f34
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 339bed0bdd386b2c871f166bb6d62efa32891474
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553107"
---
# <a name="efiusbfnmessage"></a>EFI\_USBFN\_メッセージ


**EFI\_USBFN\_メッセージ**メッセージ通知を開始したイベントを示す列挙を使用

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USBFN_MESSAGE
{
EfiUsbMsgNone = 0,
EfiUsbMsgSetupPacket,
EfiUsbMsgEndpointStatusChangedRx,
EfiUsbMsgEndpointStatusChangedTx
EfiUsbMsgBusEventDetach,
EfiUsbMsgBusEventAttach,
EfiUsbMsgBusEventReset,
EfiUsbMsgBusEventSuspend,
EfiUsbMsgBusEventResume,
EfiUsbMsgBusEventSpeed
} EFI_USBFN_MESSAGE;
```

## <a name="constants"></a>定数


<a href="" id="efiusbmsgnone"></a>**EfiUsbMsgNone**  
デバイス情報がありません。

<a href="" id="efiusbmsgsetuppacket"></a>**EfiUsbMsgSetupPacket**  
セットアップ パケットを受信し、返されたバッファーが、EFI を含むことを示します\_USB\_デバイス\_要求の構造

<a href="" id="efiusbmsgendpointstatuschangedrx"></a>**EfiUsbMsgEndpointStatusChangedRx**  
要求されたデータの一部が、ホストから受信されたことを示します。 残りのデータを待機する必要があるかどうかをクラス ドライバーの役目です。 返されたバッファーが、EFI を含む\_USBFN\_転送\_エンドポイントの数、転送の状態および受信したバイト数を含む結果の構造体。

<a href="" id="efiusbmsgendpointstatuschangedtx"></a>**EfiUsbMsgEndpointStatusChangedTx**  
要求されたデータの一部がホストに送信されたことを示します。 残りのデータを再送信する必要があるかどうかを判断するクラス ドライバーの役目です。 返されたバッファーが、EFI を含む\_USBFN\_転送\_エンドポイントの数、transferstatus および送信されたバイト数を含む結果の構造体。

<a href="" id="efiusbmsgbuseventdetach"></a>**EfiUsbMsgBusEventDetach**  
デタッチ バス イベントがシグナル状態にします。

<a href="" id="efiusbmsgbuseventattach"></a>**EfiUsbMsgBusEventAttach**  
アタッチのバスのイベントがシグナル状態にします。

<a href="" id="efiusbmsgbuseventreset"></a>**EfiUsbMsgBusEventReset**  
バス イベントがシグナル状態にリセットします。

<a href="" id="efiusbmsgbuseventsuspend"></a>**EfiUsbMsgBusEventSuspend**  
中断バス イベントがシグナル状態にします。

<a href="" id="efiusbmsgbuseventresume"></a>**EfiUsbMsgBusEventResume**  
バス イベントがシグナルを再開します。

<a href="" id="efiusbmsgbuseventspeed"></a>**EfiUsbMsgBusEventSpeed**  
バス速度が更新されると、返されたバッファーでは、バス速度を使用して示される、 [EFI\_USB\_バス\_速度](efi-usb-bus-speed.md)列挙体。

## <a name="remarks"></a>注釈


## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




