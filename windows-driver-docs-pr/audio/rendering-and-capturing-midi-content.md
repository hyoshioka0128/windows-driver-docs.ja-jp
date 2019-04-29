---
title: MIDI コンテンツのレンダリングとキャプチャ
description: MIDI コンテンツのレンダリングとキャプチャ
ms.assetid: 32eff06a-f3e8-471c-8fe6-b7cee208b90c
keywords:
- MIDI WDK オーディオのコンテンツのレンダリング
- MIDI コンテンツ WDK オーディオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dcdd1f0270492e47e0e9d583387bd797133f0ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328740"
---
# <a name="rendering-and-capturing-midi-content"></a>MIDI コンテンツのレンダリングとキャプチャ


## <span id="rendering_and_capturing_midi_content"></span><span id="RENDERING_AND_CAPTURING_MIDI_CONTENT"></span>


次の図は、コンポーネント間の関係、システムが指定した Microsoft Windows Driver Model (WDM) オーディオのレンダリングと MIDI のキャプチャをサポートするコンテンツを示しています。

![レンダリングと midi コンテンツを取り込むことを示す図](images/midi.png)

Microsoft Windows Driver Model (WDM) 音声コンポーネントの説明については、次を参照してください。

[DirectMusic システム コンポーネント](user-mode-wdm-audio-components.md#directmusic_system_component)

[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul システム ドライバー](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)

[KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[SWMidi システム ドライバー](kernel-mode-wdm-audio-components.md#swmidi_system_driver)

[DMusic システム ドライバー](kernel-mode-wdm-audio-components.md#dmusic_system_driver)

[ポート クラスのアダプターのドライバーと PortCls システム ドライバー](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

[USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)

ポート クラスのアダプターのドライバーと USBAudio ドライバーの構成に関する詳細については、次を参照してください。

[レンダリングとポートのクラスのオーディオ アダプターを使用してオーディオ コンテンツをキャプチャするには](rendering-and-capturing-audio-content-by-using-a-port-class-audio-adap.md)

[レンダリングと USBAudio ドライバーを使用してオーディオ コンテンツをキャプチャするには](rendering-and-capturing-audio-content-by-using-the-usbaudio-driver.md)

 

 




