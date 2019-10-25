---
title: オーディオ電源管理のインターフェイス
description: オーディオ電源管理のインターフェイス
ms.assetid: 7b123d3f-4f11-448e-8b20-92578fda7e69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5725675dac867ae901b45cdcbb3933916214e08
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833657"
---
# <a name="audio-power-management-interfaces"></a>オーディオ電源管理のインターフェイス


## <span id="ddk_audio_power_management_interfaces_ks"></span><span id="DDK_AUDIO_POWER_MANAGEMENT_INTERFACES_KS"></span>


ここでは、WDM オーディオアダプターの電源を管理するためにポートクラスライブラリ (portcls) で使用されるインターフェイスについて説明します。 これらのインターフェイスは、アダプタードライバーによって実装され、PortCls システムドライバーに公開されます。

次の2つのインターフェイスについて説明します。

アダプタードライバーによって実装され、オーディオアダプターカードの電源管理のために PortCls に公開されます。

アダプタードライバーによって実装され、PortCls に公開されます。 このインターフェイスは、オーディオアダプターおよびシステムに関する power managent メッセージを提供します。

低電力状態の変更を事前に通知する必要がある場合にミニポートドライバーが公開できる省略可能なインターフェイス。

[IAdapterPowerManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement)

[IAdapterPowermanagement2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement2)

[IAdapterPowerManagement3](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iadapterpowermanagement3)

[IPowerNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-ipowernotify)

 

 





