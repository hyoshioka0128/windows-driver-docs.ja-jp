---
title: デバイスの追加
description: デバイスの追加
ms.assetid: 233e3315-3044-42d7-867c-0a9e153eb53b
keywords:
- ユーザー モード ドライバー フレームワーク WDK は、デバイスの追加
- UMDF WDK、デバイスの追加
- ユーザー モード ドライバー WDK UMDF、デバイスの追加
- デバイス、WDK UMDF をインストールします。
- WDK UMDF デバイスを追加します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d27e635a27db5ff1afa0d27843a8ce6aef52b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379055"
---
# <a name="adding-a-device"></a>デバイスの追加


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは、各デバイス ドライバーのホスト プロセスで読み込まれるデバイス オブジェクトを追加します。 デバイスを追加するには、フレームワークは、ドライバーを呼び出します[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドを呼び出し、 [IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)と[IWDFDeviceInitialize。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスの呼び出しで。 指定された**IWDFDeviceInitialize**インターフェイスは、ドライバーの呼び出しの前に有効なのみ[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)します。 ドライバーは、次のメソッドを呼び出すことができます**IWDFDeviceInitialize**次の操作を実行します。

-   ドライバーの呼び出し、 [ **IWDFDeviceInitialize::RetrieveDevicePropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)を取得するメソッド、 [IWDFNamedPropertyStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore)デバイス プロパティのインターフェイスストア。 ドライバーを使用して**IWDFNamedPropertyStore**を取得して、デバイスのプロパティを設定します。

-   ドライバーの呼び出し、 [ **IWDFDeviceInitialize::SetLockingConstraint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)フレームワークによってそのコールバック関数の呼び出し方法を指定します。

-   ドライバーの呼び出し、 [ **IWDFDeviceInitialize::SetFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter)メソッド フィルター デバイスとしてデバイスを有効にします。

ドライバーは使用後[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)デバイスを初期化するために、ドライバーがへのポインターを渡す**IWDFDeviceInitialize**への呼び出しで、 [ **IWDFDriver:。CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を作成する方法、 [UMDF デバイス オブジェクト](framework-device-object.md)デバイス。 ドライバーへの呼び出しは、フレームワークのデバイス オブジェクトが作成された後、 [ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)メソッドを作成、読み取りと書き込みの I/O キュー。 これらの**IWDFDevice::CreateIoQueue** I/O キューからの要求の受信呼び出し、ドライバーを識別する必要があります。 詳細については、次を参照してください。 [I/O キューのディスパッチ モードを構成する](configuring-dispatch-mode-for-an-i-o-queue.md)します。

 

 





