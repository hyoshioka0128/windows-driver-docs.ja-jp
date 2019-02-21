---
title: オーディオの電源管理のインターフェイス
description: オーディオの電源管理のインターフェイス
ms.assetid: 7b123d3f-4f11-448e-8b20-92578fda7e69
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5448f82d5220a0a5e7891d1afcb1ef4d0b22bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551643"
---
# <a name="audio-power-management-interfaces"></a>オーディオの電源管理のインターフェイス


## <span id="ddk_audio_power_management_interfaces_ks"></span><span id="DDK_AUDIO_POWER_MANAGEMENT_INTERFACES_KS"></span>


このセクションでは、ポートのクラス ライブラリ (portcls.sys) を使用して WDM オーディオ アダプターでの電源を管理するインターフェイスについて説明します。 これらのインターフェイスはアダプタのドライバによって実装され、PortCls システム ドライバーに公開します。

次の 2 つのインターフェイスがについて説明します。

アダプタのドライバによって実装され、オーディオのアダプター カードの電源管理の PortCls に公開します。

アダプタのドライバによって実装され、PortCls に公開します。 このインターフェイスは、オーディオのアダプターと、システムの電源 managent メッセージを提供します。

省略可能なインターフェイスをミニポート ドライバーが差し迫ったの電源状態変更の事前通知が必要な場合に公開できます。

[IAdapterPowerManagement](https://msdn.microsoft.com/library/windows/hardware/ff536485)

[IAdapterPowermanagement2](https://msdn.microsoft.com/library/windows/hardware/ff536486)

[IAdapterPowerManagement3](https://msdn.microsoft.com/library/windows/hardware/jj200330)

[IPowerNotify](https://msdn.microsoft.com/library/windows/hardware/ff536947)

 

 





