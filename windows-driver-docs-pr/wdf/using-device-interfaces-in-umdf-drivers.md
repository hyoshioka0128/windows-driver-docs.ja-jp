---
title: UMDF ドライバーでのデバイス インターフェイスの使用
description: UMDF ドライバーでのデバイス インターフェイスの使用
ms.assetid: acb6da80-bd04-48f0-b42a-96463f091b0a
keywords:
- ユーザーモードドライバー WDK UMDF、デバイスインターフェイス
- UMDF WDK、デバイスインターフェイス
- ユーザーモードドライバーフレームワーク WDK、デバイスインターフェイス
- デバイスインターフェイス WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e882d43204ffae3e77ff51c4d40dea24c8e0b2b
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210778"
---
# <a name="using-device-interfaces-in-umdf-drivers"></a>UMDF ドライバーでのデバイス インターフェイスの使用


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

*デバイスインターフェイス*は、アプリケーションがデバイスにアクセスするために使用できるプラグアンドプレイ (PnP) デバイスへのシンボリックリンクです。 ユーザーモードアプリケーションは、インターフェイスのシンボリックリンク名を API 要素 (Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数など) に渡すことができます。 デバイスインターフェイスのシンボリックリンク名を取得するために、ユーザーモードアプリケーションは**Setupdi**関数を呼び出すことができます。 SetupDi 関数の詳細については、「SetupDi デバイスインターフェイス関数」を参照してください。

各デバイスインターフェイスは、*デバイスインターフェイスクラス*に属しています。 たとえば、CD-ROM デバイスのドライバースタックは、GUID\_DEVINTERFACE\_CDROM クラスに属するインターフェイスを提供する場合があります。 CD-ROM デバイスのドライバーの1つで、GUID のインスタンス\_DEVINTERFACE\_CDROM クラスが登録され、CD-ROM デバイスが使用可能であることをシステムとアプリケーションに通知します。 デバイスインターフェイスクラスの詳細については、「[デバイスインターフェイスの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)」を参照してください。

### <a name="registering-a-device-interface"></a>デバイスインターフェイスの登録

デバイスインターフェイスクラスのインスタンスを登録するために、UMDF ベースのドライバーは[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)コールバック関数内から[**Iwdfdevice:: createdeviceinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)を呼び出すことができます。 ドライバーがインターフェイスの複数のインスタンスをサポートしている場合は、一意の参照文字列を各インスタンスに割り当てることができます。

### <a name="enabling-and-disabling-a-device-interface"></a>デバイスインターフェイスを有効または無効にする

作成に成功すると、フレームワークはデバイスの PnP 状態に基づいて自動的にインターフェイスを有効または無効にします。

さらに、ドライバーは、必要に応じて、デバイスインターフェイスを無効にしてから再度有効にすることができます。 たとえば、ドライバーがデバイスの応答を停止したと判断した場合、ドライバーは[**Iwdfdevice:: 割り当て Deviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-assigndeviceinterfacestate)を呼び出してデバイスのインターフェイスを無効にし、アプリケーションがインターフェイスに新しいハンドルを取得できないようにします。 (インターフェイスに対する既存のハンドルは影響を受けません)。後でデバイスが使用可能になった場合、ドライバーは**Iwdfdevice:: 割り当て Deviceinterfacestate**を再度呼び出して、インターフェイスを再び有効にすることができます。

### <a name="receiving-requests-to-access-a-device-interface"></a>デバイスインターフェイスへのアクセス要求を受信する

アプリケーションがドライバーのデバイスインターフェイスへのアクセスを要求すると、フレームワークはドライバーの[**Iqueuecallbackcreate:: OnCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)コールバック関数を呼び出します。 ドライバーは[**Iwdffile:: RetrieveFileName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffile-retrievefilename)を呼び出して、アプリケーションがアクセスしているデバイスまたはファイルの名前を取得できます。 ドライバーがデバイスインターフェイスを登録するときに参照文字列を指定した場合、オペレーティングシステムは、 **Iwdffile:: RetrieveFileName**が返すファイル名またはデバイス名に参照文字列を含めます。

### <a name="creating-device-events"></a>デバイスイベントの作成

UMDF ベースのドライバーは、 [**Iwdfdevice::P ostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-postevent)を呼び出すことによって、デバイス固有のカスタムイベント (*デバイスイベント*と呼ばれる) を作成できます。 デバイスのインターフェイスのいずれかを使用するように登録されているドライバーは、デバイスのカスタムイベントの通知を受け取ることができます。 UMDF ベースのドライバーは、 [**IRemoteInterfaceCallbackEvent:: OnRemoteInterfaceEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)コールバック関数を提供することによって、このような通知を受け取ります。

カスタムイベントは、デバイスに固有です。 イベントを作成するドライバーの開発者と、イベントを受信するドライバーの開発者は、イベントの意味を理解している必要があります。

### <a name="accessing-another-drivers-device-interface"></a>別のドライバーのデバイスインターフェイスへのアクセス

他のドライバーが提供するデバイスインターフェイスに対して、UMDF ベースのドライバーから i/o 要求を送信する場合は、デバイスインターフェイスを表す[リモート i/o ターゲット](general-i-o-targets-in-umdf.md)を作成できます。

まず、デバイスインターフェイスが使用可能になったときに、ドライバーが通知を受け取るように登録する必要があります。 次の手順を使用します。

1.  ドライバーが[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出すと、ドライバーは[IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)インターフェイスを提供できます。 このインターフェイスの[**IPnpCallbackRemoteInterfaceNotification:: OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival) callback 関数は、デバイスインターフェイスが使用可能であることをドライバーに通知します。

2.  ドライバーは[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出した後、ドライバーが使用する各デバイスインターフェイスに対して[**IWDFDevice2:: RegisterRemoteInterfaceNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-registerremoteinterfacenotification)を呼び出すことができます。

その後、指定されたデバイスインターフェイスが使用可能になるたびに、フレームワークはドライバーの[**IPnpCallbackRemoteInterfaceNotification:: OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival) callback 関数を呼び出します。 コールバック関数は、 [**Iwdfremoteinterfaceinitialize:: GetInterfaceGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-getinterfaceguid)と[**Iwdfremoteinterfaceinitialize:: RetrieveSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-retrievesymboliclink)を呼び出して、どのデバイスインターフェイスに到達したかを判断できます。

ドライバーの[**IPnpCallbackRemoteInterfaceNotification:: OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival) callback 関数は、通常、次の操作を実行します。

1.  [**IWDFDevice2:: CreateRemoteInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-createremoteinterface)を呼び出してリモートインターフェイスオブジェクトを作成します。オプションで[IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)および[IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)インターフェイスを指定できます。

2.  [**IWDFDevice2:: CreateRemoteTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget)を呼び出してリモートターゲットオブジェクトを作成し、必要に応じて[Iremotetarget の削除](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)インターフェイスを指定します。

3.  [**Iwdfremotetarget:: OpenRemoteInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)を呼び出して、デバイスインターフェイスをリモートターゲットに接続します。

    SWENUM ソフトウェアデバイス列挙子によって作成されるデバイスインターフェイスである場合、ドライバーは作業項目から**Openremoteinterface**を呼び出す必要があります。 (例については、Windows SDK の「 **QueueUserWorkItem**関数」を参照してください)。

これで、ドライバーは、i/o 要求をフォーマットし、リモート i/o ターゲットに送信できます。

[**IPnpCallbackRemoteInterfaceNotification:: OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival) callback 関数に加えて、UMDF ベースのドライバーは、デバイスインターフェイスイベントの通知を受信するために、2つの追加のコールバック関数を提供できます。

-   [**IRemoteInterfaceCallbackRemoval:: OnRemoteInterfaceRemoval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremoteinterfacecallbackremoval-onremoteinterfaceremoval) callback 関数は、デバイスインターフェイスが削除されたことをドライバーに通知します。

-   [**IRemoteInterfaceCallbackEvent:: OnRemoteInterfaceEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)コールバック関数は、デバイスのカスタムイベントが到着したときにドライバーに通知します。

 

 





