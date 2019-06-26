---
title: オーディオ電源管理のインターフェイス
description: オーディオ電源管理のインターフェイス
ms.assetid: 7b123d3f-4f11-448e-8b20-92578fda7e69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65b4bcef0a0e841ac22fbc71df774139e1289534
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355659"
---
# <a name="audio-power-management-interfaces"></a>オーディオ電源管理のインターフェイス


## <span id="ddk_audio_power_management_interfaces_ks"></span><span id="DDK_AUDIO_POWER_MANAGEMENT_INTERFACES_KS"></span>


このセクションでは、ポートのクラス ライブラリ (portcls.sys) を使用して WDM オーディオ アダプターでの電源を管理するインターフェイスについて説明します。 これらのインターフェイスはアダプタのドライバによって実装され、PortCls システム ドライバーに公開します。

次の 2 つのインターフェイスがについて説明します。

アダプタのドライバによって実装され、オーディオのアダプター カードの電源管理の PortCls に公開します。

アダプタのドライバによって実装され、PortCls に公開します。 このインターフェイスは、オーディオのアダプターと、システムの電源 managent メッセージを提供します。

省略可能なインターフェイスをミニポート ドライバーが差し迫ったの電源状態変更の事前通知が必要な場合に公開できます。

[IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement)

[IAdapterPowermanagement2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement2)

[IAdapterPowerManagement3](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iadapterpowermanagement3)

[IPowerNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-ipowernotify)

 

 





