---
title: フレームワーク デバイス オブジェクト
description: フレームワーク デバイス オブジェクト
ms.assetid: 6be47eac-d6e4-43d1-bf2d-d49dcb2273c0
keywords:
- UMDF オブジェクト WDK、デバイス オブジェクト
- フレームワークは、WDK UMDF、デバイス オブジェクトをオブジェクトします。
- デバイス オブジェクト WDK UMDF
- IWDFDevice
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8239134e16f2ac2d7ed0f2ec31ed225d0592785
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368682"
---
# <a name="framework-device-object"></a>フレームワーク デバイス オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

Framework デバイス オブジェクトが、ドライバーに公開される、 [IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)インターフェイス。 フレームワークのデバイス オブジェクトは、システム上のデバイスのフレームワークの表現です。 各デバイス オブジェクトには、親ドライバー オブジェクトがあります。

新しいデバイスをシステムに到着すると、フレームワーク、 [ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)到着とパスのドライバーに通知するメソッド、 [IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)と[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスの呼び出しで。 ドライバーは、新しいデバイスを初期化するために IWDFDeviceInitialize インターフェイスのメソッドを呼び出すことができます。 たとえば、ドライバーは、 [ **IWDFDeviceInitialize::RetrieveDevicePropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)デバイスのインストールの一部として提供されているデバイスについては、クエリ メソッド。 ドライバーを呼び出して、 [ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドを構成し、デバイス オブジェクトを作成します。

登録するドライバーは、framework デバイス オブジェクトを作成するときに、 [IPnpCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)、 [IPnpCallbackSelfManagedIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)、 [IPnpCallbackHardware](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)、 [IFileCallbackCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ifilecallbackcleanup)、および[IFileCallbackClose](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ifilecallbackclose)インターフェイス。 フレームワークでは、ファイルのクリーンアップと終了し、プラグ アンド プレイ (PnP) と電源管理 (PM) のイベントが発生したときに、ドライバーを通知します。 PnP をサポートしていると PM の詳細については、次を参照してください。 [UMDF ベースのドライバーでの PnP と電源管理](pnp-and-power-management-in-umdf-drivers.md)します。

 

 





