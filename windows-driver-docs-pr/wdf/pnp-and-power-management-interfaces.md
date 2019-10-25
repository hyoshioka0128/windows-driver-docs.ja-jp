---
title: PnP と電源管理のインターフェイス
description: PnP と電源管理のインターフェイス
ms.assetid: b80228f7-50be-4551-870b-2d7e2b5db239
keywords:
- WDK UMDF、電源管理インターフェイスのプラグアンドプレイ
- PnP WDK UMDF、電源管理インターフェイス
- 電源管理 WDK UMDF、インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1f9a0f438ffc012a1809ded6bb7d018a9354812
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827251"
---
# <a name="pnp-and-power-management-interfaces"></a>PnP と電源管理のインターフェイス


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

新しいデバイスがシステムに到着すると、フレームワークは[**Idriverentry:: OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドを呼び出して、到着の UMDF ドライバーに通知し、呼び出しに[**Iwdfdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)および[**iwdfdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスを渡します。 ドライバーは[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドを呼び出して、デバイスのフレームワークデバイスオブジェクトを作成します。

ドライバーは、フレームワークデバイスオブジェクトを作成するときに、次のインターフェイスを登録して、プラグアンドプレイ (PnP) と電源管理 (PM) イベントが発生したときに、インターフェイスに関連付けられているメソッドを呼び出すことによって、ドライバーに通知するようにします。

[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)

[**IPowerPolicyCallbackWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

[**IPowerPolicyCallbackWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

 

 





