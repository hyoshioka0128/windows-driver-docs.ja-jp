---
title: デバイス インターフェイスの使用
description: デバイス インターフェイスの使用
ms.assetid: a41f9ae2-6128-43e2-a6b5-4d0bd45371bd
keywords:
- インターフェイス クラス WDK デバイスのインストール
- デバイスのインターフェイス クラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3fd04fd5e73bc498dc0b2202f8691b98bf05a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380446"
---
# <a name="using-a-device-interface"></a>デバイス インターフェイスの使用





デバイスのインターフェイスは、カーネル モード コンポーネントとユーザー モード アプリケーションの両方に使用します。 ユーザー モード コードで使用できる **SetupDi * * * Xxx*関数について説明する登録されている、デバイスのインターフェイスを有効にします。 参照してください[SetupDi デバイス インターフェイス関数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)詳細についてはします。

カーネル モード コンポーネントには、特定のデバイスまたはファイル オブジェクトを使用できます、前に、次の操作する必要があります。

1.  必要なデバイスのインターフェイス クラスが登録され、有効になっているかどうかを決定します。

    ドライバー、PnP マネージャー デバイス インターフェイスのインスタンスを有効または無効になっているときに通知を登録できます。 登録するコンポーネントの呼び出しに[ **IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)します。 このルーチンは、デバイス インターフェイスのインスタンスのインスタンスを有効または無効になっている、指定したデバイス クラスのたびに呼び出されるドライバーが指定したコールバックのアドレスを格納します。 コールバック ルーチンの受信、 [ **DEVICE_INTERFACE_CHANGE_NOTIFICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_interface_change_notification)構造体、インターフェイス インスタンスのシンボリック リンクを表す Unicode 文字列が含まれています。 参照してください[PnP のデバイス インターフェイスの変更通知を使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-pnp-device-interface-change-notification)詳細についてはします。

    ドライバーまたはその他のカーネル モード コンポーネントを呼び出すことも[ **IoGetDeviceInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfaces) 、登録されているすべての一覧を取得するには、デバイス インターフェイスのクラスのインスタンスを特定のデバイス インターフェイスを有効にします。 返された一覧には、デバイス インターフェイスのインスタンスを識別する Unicode シンボリック リンクの文字列へのポインターが含まれています。

2.  インターフェイスのインスタンスに対応するデバイスまたはファイル オブジェクトへのポインターを取得します。

    特定のデバイス オブジェクトにアクセスするドライバーを呼び出す必要があります[ **IoGetDeviceObjectPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)、必要なインターフェイスでの Unicode 文字列を渡す、 *ObjectName*パラメーター。 ファイル オブジェクトにアクセスするドライバーを呼び出す必要があります[ **InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes)での Unicode 文字列を渡す、 *ObjectName*パラメーターであり、パス、正常に呼び出しに属性の構造を初期化[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)します。

 

 





