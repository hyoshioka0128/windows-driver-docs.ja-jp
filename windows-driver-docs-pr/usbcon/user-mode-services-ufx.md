---
Description: I/o 制御コード (IOCTL) 要求を送信して、GenericUSBFn と通信するユーザーモードサービスを作成します。
title: ユーザーモード サービスから GenericUSBFn.sys と通信する
ms.date: 07/26/2019
ms.localizationpriority: medium
ms.openlocfilehash: fa8b95867d129f49ad4abe4f294784eb77461dba
ms.sourcegitcommit: d7be945c4168756d5c11623b8ffb2880834d8382
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2019
ms.locfileid: "68590938"
---
# <a name="communicating-with-genericusbfnsys-from-a-user-mode-service"></a>ユーザーモード サービスから GenericUSBFn.sys と通信する 


すべてのユーザーモード要求は、Microsoft が提供するカーネルモードドライバーの GenericUSBFn に送信されます。 これらの i/o 制御コード (IOCTL) を送信することで GenericUSBFn と通信するユーザーモードサービスを作成できます。また、GenericUSBFn は、USB 関数ドライバーとのカーネルモード通信を処理します。

[Genericusbfに](https://docs.microsoft.com/windows/desktop/api/genericusbfnioctl/)宣言された ioctl は、ユーザーモードサービスからの GenericUSBFn との通信に使用されます。


次の手順では、GenericUSBFn とやり取りして USB 関数ドライバーと通信する、USB インターフェイスサービスを定義する方法について説明します。

1. 起動時に、サービスはインターフェイスのデバイスインターフェイスの到着をリッスンします。 デバイスインターフェイス GUID は、HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\USBFN\Interfaces. の OEM 定義サブキーの下にあるレジストリで宣言されている InterfaceGUID 値です。 デバイスの到着をリッスンするには、次の2つの一般的な方法があります。
    - トリガーサービスを開始します。 詳細については、「サービストリガーイベント」を参照してください。 
    - デバイスインターフェイスへの到着を登録します。 詳細については、「CM_Register_Notification 関数」を参照してください。 
2. インターフェイスが到着すると、サービスはデバイスへのハンドルを開きます。 
    - CM_Get_Device_Interface_List 関数を呼び出して、デバイスのシンボル名を取得します。 レジストリの InterfaceGUID 値で宣言されているデバイスインターフェイス GUID を指定します。
    - デバイスのシンボル名を取得したら、CreateFile を使用してデバイスへのハンドルを開きます。 
3. このサービスは、レジストリで構成されている使用可能なパイプに関する情報を取得するために IOCTL_GENERICUSBFN_GET_CLASS_INFO を発行します。 
4. サービスが通信する準備が整うと、IOCTL_GENERICUSBFN_ACTIVATE_USB_BUS が発行されます。 すべてのクラスドライバーがアクティブ化された後、USB 関数クラス拡張はホストに接続できます。 
5. USB 通知を受信するために、サービスは IOCTL_GENERICUSBFN_BUS_EVENT_NOTIFICATION を発行します。 この IOCTL は、新しい USB イベントが発生したときに完了します。 特に興味のあるイベント (USBFN_EVENT) は次のとおりです。
6. UsbfnEventReset:これは、接続されている USB デバイスの速度を決定するために使用されます。 
7. UsbfnEventConfigured:サービスは、転送要求を発行できるようになりました。 
8. UsbfnEventSetupPacket:USB 関数クラス拡張は、インターフェイス固有のセットアップパケット (bmRequestType. Type = = BMREQUEST_CLASS) を受信しました。 サービスは、パイプ0で転送要求を発行し、パイプ0の逆方向のハンドシェイク要求 (IOCTL_GENERICUSBFN_CONTROL_STATUS_HANDSHAKE_OUT) を実行して、セットアップパケットに応答する必要があります。 
9. UsbfnEventConfigured イベントが受信されると、サービスは IOCTL_GENERICUSBFN_TRANSFER_IN、IOCTL_GENERICUSBFN_TRANSFER_IN_APPEND_ZERO_PKT、および IOCTL_GENERICUSBFN_TRANSFER_OUT を使用して転送要求の発行を開始できます。 
