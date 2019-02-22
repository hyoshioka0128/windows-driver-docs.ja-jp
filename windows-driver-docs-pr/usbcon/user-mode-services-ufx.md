---
Description: Create a user-mode service that communicates with GenericUSBFn.sys by sending I/O control code (IOCTL) requests.
title: ユーザー モード サービスから GenericUSBFn.sys との通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 638ad0ddee69f42aff323eb13195a744317214b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552736"
---
# <a name="communicating-with-genericusbfnsys-from-a-user-mode-service"></a>ユーザー モード サービスから GenericUSBFn.sys との通信 


ユーザー モードのすべての要求は、Microsoft から提供されたカーネル モード ドライバー GenericUSBFn.sys に送信されます。 USB 機能ドライバーとカーネル モードの通信にこれらの I/O 制御コード (IOCTL) と GenericUSBFn.sys ハンドルを送信することによって GenericUSBFn.sys で通信を行うユーザー モード サービスを作成できます。

宣言されている Ioctl [Genericusbfnioctl.h](https://docs.microsoft.com/windows/desktop/api/genericusbfnioctl/) GenericUSBFn.sys とユーザー モード サービスから通信するために使用します。


次の手順では、USB 機能ドライバーとの通信に GenericUSBFn.sys と連携する USB インターフェイス サービスを定義する方法について説明します。

1. スタートアップ時に、サービスは、インターフェイスのデバイスのインターフェイスの到着をリッスンします。 デバイス インターフェイスの GUID は、OEM が定義した HKEY_LOCAL_MACHINE\CurrentControlSet\Control\USBFN\Interfaces のサブキーの下のレジストリで宣言されている InterfaceGUID 値です。 デバイスの到着をリッスンする 2 つの一般的な方法はあります。
    - トリガーは、サービスを開始します。 詳細については、サービスのトリガー イベントを参照してください。 
    - デバイス インターフェイスの到着に登録します。 詳細については、CM_Register_Notification 関数を参照してください。 
2. インターフェイスが到着すると、サービスは、デバイスを識別するハンドルを開きます。 
    - CM_Get_Device_Interface_List 関数を呼び出すことによって、デバイスのシンボリック名を取得します。 レジストリの InterfaceGUID 値では、デバイス インターフェイスが宣言されている GUID を指定します。
    - デバイスのシンボリック名を取得したら、CreateFile でデバイスを識別するハンドルを開きます。 
3. サービスは、レジストリで構成されている IOCTL_GENERICUSBFN_GET_CLASS_INFO 利用可能なパイプに関する情報を取得するを発行します。 
4. サービスと通信する準備ができたら後、は、IOCTL_GENERICUSBFN_ACTIVATE_USB_BUS を発行します。 すべてのクラス ドライバーを有効にしたら、USB 関数クラスの拡張機能は、ホストに接続できます。 
5. USB の通知を受信するには、サービスは、IOCTL_GENERICUSBFN_BUS_EVENT_NOTIFICATION を発行します。 新しい USB イベントが発生したときに、この IOCTL が完了します。 特定の関心のあるイベント (USBFN_EVENT) は次のとおりです。
6. UsbfnEventReset:これは、接続された USB デバイスの速度を決定に使用されます。 
7. UsbfnEventConfigured:サービスでは、転送要求を発行できますようになりました。 
8. UsbfnEventSetupPacket:USB 関数クラスの拡張機能がインターフェイスに固有のセットアップ パケットを受信しました (bmRequestType.Type BMREQUEST_CLASS = =)。 サービスは、0 をパイプで逆方向にハンドシェイク要求 (IOCTL_GENERICUSBFN_CONTROL_STATUS_HANDSHAKE_OUT) 後に 0、パイプの転送要求を発行することによってセットアップ パケットに返信する必要があります。 
9. UsbfnEventConfigured イベントを受信すると、サービスが IOCTL_GENERICUSBFN_TRANSFER_IN、IOCTL_GENERICUSBFN_TRANSFER_IN_APPEND_ZERO_PKT、IOCTL_GENERICUSBFN_TRANSFER_OUT を使用して転送要求を発行を開始することができます。 
