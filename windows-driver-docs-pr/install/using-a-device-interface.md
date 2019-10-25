---
title: デバイス インターフェイスの使用
description: デバイス インターフェイスの使用
ms.assetid: a41f9ae2-6128-43e2-a6b5-4d0bd45371bd
keywords:
- インターフェイスクラス WDK デバイスのインストール
- デバイスインターフェイスクラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2d98c7851a8b735f2926f130f624d1cb84849e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837351"
---
# <a name="using-a-device-interface"></a>デバイス インターフェイスの使用





デバイスインターフェイスは、カーネルモードコンポーネントとユーザーモードアプリケーションの両方で使用できます。 ユーザーモードのコードでは、**Setupdi * * * Xxx*関数を使用して、登録済みの有効なデバイスインターフェイスを調べることができます。 詳細については、「 [Setupdi デバイスインターフェイス関数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)」を参照してください。

カーネルモードコンポーネントが特定のデバイスまたはファイルオブジェクトを使用できるようにするには、次の操作を行う必要があります。

1.  必要なデバイスインターフェイスクラスが登録され、有効になっているかどうかを確認します。

    ドライバーは、デバイスインターフェイスのインスタンスが有効または無効になったときに通知を受けるように、PnP マネージャーに登録できます。 登録するために、コンポーネントは[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出します。 このルーチンは、指定されたデバイスクラスについて、デバイスインターフェイスインスタンスのインスタンスが有効または無効になるたびに呼び出される、ドライバーによって提供されるコールバックのアドレスを格納します。 コールバックルーチンは、インターフェイスインスタンスのシンボリックリンクを表す Unicode 文字列を含む[**DEVICE_INTERFACE_CHANGE_NOTIFICATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_interface_change_notification)構造体を受け取ります。 詳細については、「 [PnP デバイスインターフェイス変更通知の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-pnp-device-interface-change-notification)」を参照してください。

    ドライバーまたはその他のカーネルモードコンポーネントは、 [**Iogetdeviceinterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)を呼び出して、特定のデバイスインターフェイスクラスの登録済みの有効なデバイスインターフェイスインスタンスの一覧を取得することもできます。 返される一覧には、デバイスインターフェイスインスタンスを識別する Unicode シンボリックリンク文字列へのポインターが含まれています。

2.  インターフェイスのインスタンスに対応するデバイスまたはファイルオブジェクトへのポインターを取得します。

    特定のデバイスオブジェクトにアクセスするには、ドライバーが[**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)を呼び出し、必要なインターフェイスの Unicode 文字列を*ObjectName*パラメーターに渡す必要があります。 ファイルオブジェクトにアクセスするには、ドライバーは[**Initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)を呼び出し、 *ObjectName*パラメーターで Unicode 文字列を渡し、 [**zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)への呼び出しで正常に初期化された属性構造を渡す必要があります。

 

 





