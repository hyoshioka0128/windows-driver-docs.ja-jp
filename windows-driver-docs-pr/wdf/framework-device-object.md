---
title: フレームワーク デバイス オブジェクト
description: フレームワーク デバイス オブジェクト
ms.assetid: 6be47eac-d6e4-43d1-bf2d-d49dcb2273c0
keywords:
- UMDF オブジェクト WDK、デバイスオブジェクト
- フレームワークオブジェクト WDK UMDF、デバイスオブジェクト
- デバイスオブジェクト WDK UMDF
- IWDFDevice
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0008ec6cc16be804627815954684d443a7faeb35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843183"
---
# <a name="framework-device-object"></a>フレームワーク デバイス オブジェクト


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークデバイスオブジェクトは、 [Iwdfdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスによってドライバーに公開されます。 Framework device オブジェクトは、システム上のデバイスのフレームワーク表現です。 各デバイスオブジェクトには親ドライバーオブジェクトがあります。

新しいデバイスがシステムに到着すると、フレームワークは[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドを呼び出して、到着をドライバーに通知し、呼び出しの[Iwdfdriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)インターフェイスと[iwdfdeviceinitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスを渡します。 ドライバーは、IWDFDeviceInitialize インターフェイスのメソッドを呼び出して、新しいデバイスを初期化することができます。 たとえば、ドライバーは[**Iwdfdeviceinitialize:: RetrieveDevicePropertyStore**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)メソッドを呼び出して、デバイスのインストールの一部として提供されているデバイス情報を照会します。 その後、ドライバーは[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドを呼び出して、デバイスオブジェクトを構成および作成できます。

ドライバーは、フレームワークのデバイスオブジェクトを作成するときに、 [IPnpCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)、 [IPnpCallbackSelfManagedIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)、 [IPnpCallbackHardware](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)、 [IFileCallbackCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ifilecallbackcleanup)、および[IFileCallbackClose](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ifilecallbackclose)の各インターフェイスを登録できます。 次に、ファイルのクリーンアップと終了とプラグアンドプレイ (PnP) と電源管理 (PM) イベントが発生したときに、フレームワークによってドライバーに通知されます。 PnP と PM のサポートの詳細については、「 [UMDF And 電源管理](pnp-and-power-management-in-umdf-drivers.md)」を参照してください。

 

 





