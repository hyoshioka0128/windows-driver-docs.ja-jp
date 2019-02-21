---
title: レンダリングと Wave コンテンツをキャプチャします。
description: レンダリングと Wave コンテンツをキャプチャします。
ms.assetid: 575499a9-e572-4ccc-bcee-8f2843310b05
keywords:
- wave WDK オーディオのレンダリング
- wave キャプチャ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d4466631153a102d59b373eebc2cba6984a7c59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531044"
---
# <a name="rendering-and-capturing-wave-content"></a>レンダリングと Wave コンテンツをキャプチャします。


## <span id="rendering_and_capturing_wave_content"></span><span id="RENDERING_AND_CAPTURING_WAVE_CONTENT"></span>


次の図は、レンダリング、wave コンテンツをキャプチャする Microsoft Windows Driver Model (WDM) オーディオ コンポーネントの構成を示します。

![レンダリングと wave コンテンツを取り込むことを示す図](images/wave.png)

WDM オーディオ コンポーネントの説明については、次を参照してください。

[DirectSound システム コンポーネント](user-mode-wdm-audio-components.md#directsound_system_component)

[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul システム ドライバー](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook システム ドライバー](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[スプリッター システム ドライバー](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[ポート クラスのアダプターのドライバーと PortCls システム ドライバー](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

ポート クラスのアダプターのドライバーと USBAudio ドライバーの構成に関する詳細については、次を参照してください。

[レンダリングとポートのクラスのオーディオ アダプターを使用してオーディオ コンテンツをキャプチャするには](rendering-and-capturing-audio-content-by-using-a-port-class-audio-adap.md)

[レンダリングと USBAudio ドライバーを使用してオーディオ コンテンツをキャプチャするには](rendering-and-capturing-audio-content-by-using-the-usbaudio-driver.md)

 

 




