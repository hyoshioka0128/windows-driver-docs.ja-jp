---
title: PnP と電源管理のインターフェイス
description: PnP と電源管理のインターフェイス
ms.assetid: b80228f7-50be-4551-870b-2d7e2b5db239
keywords:
- プラグ アンド プレイ WDK UMDF、電源管理のインターフェイス
- PnP WDK UMDF、電源管理のインターフェイス
- 電源管理 WDK UMDF、インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a43df368b6effbb89980b8a45872316713a62c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379662"
---
# <a name="pnp-and-power-management-interfaces"></a>PnP と電源管理のインターフェイス


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

新しいデバイスをシステムに到着すると、フレームワーク、 [ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)到着とパスの UMDF ドライバーに通知するメソッド、 [ **IWDFDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)と[ **IWDFDeviceInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)インターフェイスの呼び出しで。 ドライバーの呼び出し、 [ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice) framework デバイスのデバイス オブジェクトを作成するメソッド。

フレームワーク、ドライバーに通知するために、次のインターフェイスを登録するドライバーは、framework デバイス オブジェクトを作成するときに、インターフェイスに関連付けられているメソッドを呼び出して、— プラグ アンド プレイ (PnP) および電源管理 (PM) のイベントが発生します。

[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)

[**IPowerPolicyCallbackWakeFromS0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefroms0)

[**IPowerPolicyCallbackWakeFromSx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipowerpolicycallbackwakefromsx)

 

 





