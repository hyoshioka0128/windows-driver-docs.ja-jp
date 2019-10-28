---
title: 制御デバイス オブジェクトの使用
description: 制御デバイス オブジェクトの使用
ms.assetid: 6367954f-6916-46df-a5a0-e80f045b69e5
keywords:
- デバイスオブジェクトの管理 (WDK KMDF)
- デバイスオブジェクト WDK KMDF
- フレームワークオブジェクト WDK KMDF、デバイスオブジェクトの制御
- レガシハードウェアデバイス WDK KMDF
- ソフトウェアのみの仮想デバイス WDK KMDF
- システムシャットダウン通知 WDK KMDF
- シャットダウン通知 WDK KMDF
- 通知 WDK KMDF
- WDK KMDF の名前
- WDK KMDF、デバイスオブジェクトの名前
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2ad389ff85a4ec918802dcf30d5f389edd20ff7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843094"
---
# <a name="using-control-device-objects"></a>制御デバイス オブジェクトの使用


*コントロールデバイスオブジェクト*は、プラグアンドプレイ (PnP) 操作または電源管理操作をサポートしないフレームワークデバイスオブジェクトです。 ドライバーは、コントロールデバイスオブジェクトを使用して、ソフトウェアのみの仮想デバイスまたは*レガシハードウェアデバイス*(つまり、PnP または電源管理機能を提供しないデバイス) を表すことができます。

コントロールデバイスオブジェクトを作成するドライバーも、通常、デバイスオブジェクトのシンボリックリンクを作成します。 アプリケーションは、Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数などの API 要素にシンボリックリンク名を渡すことによって、コントロールデバイスオブジェクトに i/o 要求を送信できます。

フレームワークは、[デバイススタック](wdm-concepts-for-kmdf-drivers.md#device-stacks)にコントロールデバイスオブジェクトをアタッチしません。 このため、アプリケーションからコントロールデバイスオブジェクトに i/o 要求を送信すると、i/o マネージャーは、スタックの一番上にあるドライバーではなく、コントロールデバイスオブジェクトを作成したドライバーに要求を直接配信します。 (ただし、追加のドライバーは[**Ioattachdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)を呼び出して、コントロールデバイスオブジェクトの上にデバイスオブジェクトをアタッチできます。 この場合、追加のドライバーは最初に i/o 要求を受け取ります)。

### <a name="uses-of-control-device-objects"></a>コントロールデバイスオブジェクトの使用

コントロールデバイスの一般的な用途は次の2つです。

1.  アプリケーションが使用するカスタム i/o 制御コードのセットをドライバーがサポートしている場合は、PnP デバイス用のフィルタードライバー。

    アプリケーションがカスタム i/o 制御コードをドライバースタックの一番上に送信しようとした場合 (たとえば、[デバイスインターフェイス](using-device-interfaces.md)のシンボリックリンク名を使用して)、フィルタードライバーの上にあるドライバーは、ドライバーが次を認識しなかった場合に i/o 要求を失敗させる可能性があります。カスタム i/o 制御コード。 この問題を回避するには、フィルタードライバーでコントロールデバイスオブジェクトを作成します。 アプリケーションでは、コントロールデバイスオブジェクトのシンボリックリンク名を使用して、フィルタードライバーに i/o 制御コードを直接送信できます。

    (フィルタードライバーが問題を回避するには、バスドライバーとして機能し、raw モードで動作する子デバイスを[列挙](enumerating-the-devices-on-a-bus.md)する方が適切な方法であることに注意してください。 つまり、フィルタードライバーがサポートするデバイスごとに、ドライバーは、関数ドライバーを必要としない物理デバイスオブジェクト (PDO) を作成できます。 ドライバーは、これらの各デバイスに対して[**Wdfpdoinit割り当て Rawdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)と[**wdfdeviceinit割り当て名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)を呼び出します。アプリケーションは、カスタム i/o 制御コードを送信するときに、名前を指定してデバイスを識別できます。

2.  PnP をサポートしていないデバイスのドライバー。

    このようなドライバーでは、コントロールデバイスオブジェクトを使用する必要があります。これは、このようなデバイスのデバイスオブジェクトがデバイススタックに存在せず、PnP 機能を提供しないためです。 非 PnP デバイスのサポートの詳細については、「[カーネルモードドライバーフレームワークと非 Pnp ドライバーの使用](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)」を参照してください。

### <a name="creating-a-control-device-object"></a>コントロールデバイスオブジェクトの作成

コントロールデバイスオブジェクトを作成するには、ドライバーが次の操作を行う必要があります。

1.  [**Wdfcontroldeviceinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitallocate)を呼び出して、 [**wdfdevice\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体を取得します。

2.  必要に応じて、オブジェクトの初期化メソッドを呼び出して、WDFDEVICE\_INIT 構造体を初期化します。 ドライバーは、次の初期化メソッドのみを呼び出すことができます。
    -   [**WdfControlDeviceInitSetShutdownNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitsetshutdownnotification)
    -   [**Wdfdeviceinit割り当て名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)
    -   [**Wdfdeviceinit割り当て Sddlstring**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)
    -   [**Wdfdeviceinit割り当て Wdmirpq Preprocesscallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback)
    -   [**WdfDeviceInitSetCharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetcharacteristics)
    -   [**WdfDeviceInitSetDeviceClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)
    -   [**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)
    -   [**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)
    -   [**WdfDeviceInitSetIoInCallerContextCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetioincallercontextcallback)
    -   [**WdfDeviceInitSetIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotype)
    -   [**WdfDeviceInitSetRequestAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes)

3.  [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出します。これは、WDFDEVICE\_INIT 構造体の内容を使用して、フレームワークデバイスオブジェクトを作成します。

4.  次の初期化操作を完了します。
    -   デバイスの[既定の i/o キューを作成](creating-i-o-queues.md)します (必要な場合)。
    -   必要に応じて、 [**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)を呼び出します。
    -   [**WdfDeviceCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)を呼び出して、アプリケーションがコントロールデバイスにアクセスするために使用できるシンボリックリンク名を作成します。

5.  [**Wdfcontrolfinish**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontrolfinishinitializing)を呼び出します。

### <a name="rules-for-using-control-device-objects"></a>コントロールデバイスオブジェクトを使用するための規則

コントロールデバイスオブジェクトを作成するドライバーは、次の規則に従う必要があります。

-   ドライバーは、[子デバイスを列挙](enumerating-the-devices-on-a-bus.md)するフレームワークメソッドにコントロールデバイスオブジェクトのハンドルを渡すことはできません。

-   ドライバーは、[デバイスインターフェイス](using-device-interfaces.md)をサポートするフレームワークメソッドにコントロールデバイスオブジェクトのハンドルを渡すことはできません。

-   ドライバーは、i/o キューを作成し、キューの要求ハンドラーを登録できますが、このフレームワークでは、キューの[電源管理](using-power-managed-i-o-queues.md)を許可していません。

-   ドライバーは、コントロールデバイスオブジェクトの[ファイルオブジェクト](framework-file-objects.md)を作成できます。

### <a name="naming-a-control-device-object"></a>コントロールデバイスオブジェクトの名前付け

すべてのコントロールデバイスオブジェクトに名前を付ける必要があります。 通常、ドライバーは[**Wdfdeviceinitassign name**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)を呼び出してデバイス名を割り当て、次に[**WdfDeviceCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)を呼び出して、アプリケーションがオブジェクトにアクセスするために使用できるシンボリックリンク名を作成します。

ドライバーが[**Wdfdeviceinitassign name**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)を呼び出してデバイス名を割り当てない場合、フレームワークはコントロールデバイスの名前を自動的に生成しますが、ドライバーは[**WdfDeviceCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)を呼び出すことができません。

ドライバーは、 [**Wdfdeviceinitsetdeviceclass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)を呼び出して、コントロールデバイスの[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)を指定できます。 デバイスセットアップクラスは、セットアップクラスに属するデバイスに関する管理者によって提供される情報を含むレジストリのセクションを識別します。 [**Wdfdeviceinitsetdeviceclass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)の呼び出しの詳細については、「[フレームワークベースのドライバーでデバイスアクセスを制御](controlling-device-access-in-kmdf-drivers.md)する」を参照してください。

### <a name="receiving-notification-of-system-shutdown"></a>システムシャットダウンの通知を受信しています

コントロールデバイスオブジェクトでは PnP がサポートされていないため、デバイスの電源状態が変化したときにドライバーに通知するコールバック関数をドライバーで登録することはできません。 ただし、ドライバーは、 [**Wdfcontroldeviceinitsetshutdownnotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nf-wdfcontrol-wdfcontroldeviceinitsetshutdownnotification)を呼び出して、 [*evtdeviceの通知*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcontrol/nc-wdfcontrol-evt_wdf_device_shutdown_notification)コールバック関数を登録できます。 このコールバック関数は、システムの電源が切れようとしていることをドライバーに通知します。

### <a name="deleting-a-control-device-object"></a>コントロールデバイスオブジェクトの削除

ドライバーによっては、次のように、ドライバーがアンロードされる前にコントロールデバイスオブジェクトを削除する必要があります。

-   ドライバーがコントロールデバイスオブジェクト (PnP または電源管理をサポートしていない) を作成し、PnP と電源管理をサポートするフレームワークデバイスオブジェクトもドライバーによって作成されている場合、ドライバーは最終的に IRQL = PASSIVE で[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出す必要があります。コントロールデバイスオブジェクトを削除する\_レベル。

    ドライバーが両方の種類のデバイスオブジェクトを作成した場合、ドライバーがコントロールデバイスオブジェクトを削除するまで、オペレーティングシステムはドライバーをアンロードできません。

    ただし、その他のデバイスオブジェクトがフレームワークによって削除されるまで、ドライバーはコントロールデバイスオブジェクトを削除しないでください。 他のデバイスオブジェクトがフレームワークによって削除されたことを確認するには、ドライバーがこれらのオブジェクトに対して[*Evtcleanupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)関数を提供する必要があります。

-   ドライバーがコントロールデバイスオブジェクトを作成しても、PnP と電源管理をサポートするフレームワークデバイスオブジェクトを作成しない場合、ドライバーはコントロールデバイスオブジェクトを削除する必要はありません。

    この場合、ドライバーの[*Evtdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)コールバック関数から制御が戻った後に、フレームワークによってコントロールデバイスオブジェクトが削除されます。

 

 





