---
title: UMDF ドライバーでのデバイス インターフェイスの使用
description: UMDF ドライバーでのデバイス インターフェイスの使用
ms.assetid: acb6da80-bd04-48f0-b42a-96463f091b0a
keywords:
- ユーザー モード ドライバー WDK UMDF、デバイス インターフェイス
- UMDF WDK、デバイス インターフェイス
- ユーザー モード ドライバー フレームワーク WDK、デバイス インターフェイス
- デバイスは、WDK UMDF をインターフェイスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6c8695e09c548b168af7bb8b2d084f5c6eb4995
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372279"
---
# <a name="using-device-interfaces-in-umdf-drivers"></a>UMDF ドライバーでのデバイス インターフェイスの使用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

A*デバイス インターフェイス*プラグ アンド プレイ (PnP) へのシンボリック リンクは、デバイス、デバイスにアクセスするアプリケーションで使用できます。 ユーザー モード アプリケーションは、Microsoft Win32 などの API 要素に、インターフェイスのシンボリック リンクの名前を渡すことができます[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数。 ユーザー モード アプリケーションを呼び出して、デバイス インターフェイスのシンボリック リンクの名前を取得する**SetupDi**関数。 SetupDi 関数の詳細については、SetupDi デバイス インターフェイスの関数を参照してください。

各デバイスのインターフェイスが属する、*デバイス インターフェイス クラス*します。 たとえば、CD-ROM デバイスのドライバー スタックは、GUID が属しているインターフェイスを提供可能性があります\_DEVINTERFACE\_CDROM クラス。 CD-ROM デバイスのドライバーの 1 つは、GUID のインスタンスを登録\_DEVINTERFACE\_CD-ROM デバイスが使用可能なシステムおよびアプリケーションに通知する CDROM クラス。 デバイスのインターフェイス クラスの詳細については、次を参照してください。[デバイス インターフェイスの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)します。

### <a name="registering-a-device-interface"></a>デバイスのインターフェイスを登録します。

デバイスのインターフェイス クラスのインスタンスを登録するには、UMDF ドライバーを呼び出すことができます[ **IWDFDevice::CreateDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)内からその[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数。 ドライバーでは、インターフェイスの複数のインスタンスをサポートする場合は、各インスタンスに一意の参照文字列を割り当てることができます。

### <a name="enabling-and-disabling-a-device-interface"></a>有効にして、デバイスのインターフェイスを無効化

作成が成功すると、フレームワークによって自動的に有効にし、デバイスの PnP 状態に基づくインターフェイスを無効にします。

さらに、ドライバーは無効にし、必要に応じて、デバイス インターフェイスを再度有効にすることができます。 たとえば、ドライバーは、そのデバイスが応答を停止したことを判断した場合、ドライバー呼び出すことができます[ **IWDFDevice::AssignDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-assigndeviceinterfacestate)デバイスのインターフェイスを無効にして、禁止するにはアプリケーション インターフェイスに新しいハンドルを取得します。 (既存のハンドルをインターフェイスには影響はありません)。ドライバーを呼び出すことができます、デバイスが後で使用可能なになると、 **IWDFDevice::AssignDeviceInterfaceState**インターフェイスを再度有効にするには、もう一度です。

### <a name="receiving-requests-to-access-a-device-interface"></a>デバイス インターフェイスへのアクセス要求の受信

アプリケーションでは、ドライバーのデバイス インターフェイスへのアクセスを要求、フレームワークのドライバーの[ **IQueueCallbackCreate::OnCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)コールバック関数。 ドライバーを呼び出すことができます[ **IWDFFile::RetrieveFileName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdffile-retrievefilename)デバイスやアプリケーションにアクセスしているファイルの名前を取得します。 オペレーティング システムにはファイルに参照文字列が含まれています、ドライバーで、デバイス インターフェイスが登録されているときに参照文字列を指定する場合、またはデバイス名を**IWDFFile::RetrieveFileName**を返します。

### <a name="creating-device-events"></a>デバイス イベントの作成

UMDF ドライバーは、デバイスに固有のカスタム イベントを作成できます (と呼ばれる*デバイス イベント*) を呼び出して[ **IWDFDevice::PostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-postevent)します。 デバイスのインターフェイスのいずれかを使用する登録されているドライバーでは、デバイスのカスタム イベントの通知を受信できます。 UMDF ベースのドライバーが提供することでこのような通知を受信する[ **IRemoteInterfaceCallbackEvent::OnRemoteInterfaceEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)コールバック関数。

カスタム イベントは、デバイスに固有です。 イベントを作成するドライバーの開発者と、イベントを受信するドライバーの開発者の両方では、イベントの意味を理解する必要があります。

### <a name="accessing-another-drivers-device-interface"></a>別のドライバーのデバイス インターフェイスへのアクセス

UMDF ベースのドライバーをデバイス インターフェイスへの I/O 要求を送信する場合は、その他のドライバーを提供、作成することができます、[リモートの I/O ターゲット](general-i-o-targets-in-umdf.md)デバイス インターフェイスを表します。

最初に、ドライバーは、デバイス インターフェイスが使用可能な場合に通知を受信登録する必要があります。 次の手順を使用します。

1.  ドライバーを呼び出すと[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)、ドライバーが提供できる、 [IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)インターフェイス。 [ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)デバイス インターフェイスが使用可能な場合にこのインターフェイスのコールバック関数が、ドライバーに通知します。

2.  ドライバーの呼び出し後[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)、呼び出すことができます[ **IWDFDevice2::RegisterRemoteInterfaceNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-registerremoteinterfacenotification)インターフェイスの各デバイス ドライバーは使用してください。

その後、フレームワークが、ドライバーの[ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)コールバック関数を指定したデバイスのインターフェイスになるたびにご利用いただけます。 コールバック関数を呼び出すことができます[ **IWDFRemoteInterfaceInitialize::GetInterfaceGuid** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-getinterfaceguid)と[ **IWDFRemoteInterfaceInitialize::RetrieveSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-retrievesymboliclink)インターフェイスが到着するデバイスを決定します。

ドライバーの[ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)コールバック関数は、次を行う通常必要があります。

1.  呼び出す[ **IWDFDevice2::CreateRemoteInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-createremoteinterface)必要に応じて提供するリモート インターフェイス オブジェクトを作成する[IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)と[IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)インターフェイス。

2.  呼び出す[ **IWDFDevice2::CreateRemoteTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget)オプションを提供する、リモート ターゲット オブジェクトを作成する、 [IRemoteTargetCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)インターフェイス。

3.  呼び出す[ **IWDFRemoteTarget::OpenRemoteInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)デバイス インターフェイスをリモート ターゲットに接続します。

    デバイスのインターフェイスが SWENUM ソフトウェア デバイスの列挙子を作成する 1 つの場合、ドライバーを呼び出す必要があります**OpenRemoteInterface**作業項目から。 (たとえばを参照してください、 **QueueUserWorkItem** Windows SDK 内の関数です)。

今すぐドライバーは、書式を設定し、リモートの I/O ターゲットに I/O 要求を送信します。

加え、 [ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)コールバック関数では、UMDF ドライバーは、受信する 2 つの追加のコールバック関数を提供できますデバイス インターフェイスのイベントの通知:

-   [ **IRemoteInterfaceCallbackRemoval::OnRemoteInterfaceRemoval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremoteinterfacecallbackremoval-onremoteinterfaceremoval)デバイス インターフェイスが削除されたときにコールバック関数は、ドライバーに通知します。

-   [ **IRemoteInterfaceCallbackEvent::OnRemoteInterfaceEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)コールバック関数は、デバイスのカスタム イベントが到着したときに、ドライバーを通知します。

 

 





