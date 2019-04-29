---
title: レンダリングとポート クラス オーディオ アダプターを使用してオーディオをキャプチャします。
description: レンダリングとポート クラス オーディオ アダプターを使用してオーディオをキャプチャします。
ms.assetid: a6f47f94-eaff-47bf-b9e5-fc6d4b8d25fd
keywords:
- ポート クラス アダプター ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 645dd01cbe0ffd19fbce5d22d60a2f4bb2df89bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328722"
---
# <a name="rendering-and-capturing-audio-content-by-using-a-port-class-audio-adapter"></a>ポート クラスのオーディオ アダプターを使用したオーディオ コンテンツのレンダリングとキャプチャ


## <span id="ddk_rendering_and_capturing_audio_content_by_using_a_port_class_audio_"></span><span id="DDK_RENDERING_AND_CAPTURING_AUDIO_CONTENT_BY_USING_A_PORT_CLASS_AUDIO_"></span>


次の図は、レンダリングし、オーディオ コンテンツをキャプチャするポート クラス オーディオ アダプター ドライバーの構成を示します。

![レンダリングとポートのクラスのオーディオ アダプター ドライバーを使用してオーディオ コンテンツを取り込むことを示す図](images/portcls.png)

Microsoft Windows Driver Model (WDM) 音声コンポーネントの説明については、次を参照してください。

[DirectSound システム コンポーネント](user-mode-wdm-audio-components.md#directsound_system_component)

[DirectMusic システム コンポーネント](user-mode-wdm-audio-components.md#directmusic_system_component)

[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul システム ドライバー](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook システム ドライバー](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[スプリッター システム ドライバー](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[ポート クラスのアダプターのドライバーと PortCls システム ドライバー](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)

Wave、MIDI、DirectMusic、およびフィルターのトポロジについては、次を参照してください。

[Wave フィルター](wave-filters.md)

[MIDI と DirectMusic フィルター](midi-and-directmusic-filters.md)

[トポロジのフィルター](topology-filters.md)

ポート クラス オーディオ アダプター上にあるフィルター グラフの詳細については、次を参照してください。

[レンダリングと Wave コンテンツをキャプチャします。](rendering-and-capturing-wave-content.md)

[レンダリングと MIDI コンテンツをキャプチャします。](rendering-and-capturing-midi-content.md)

 

 




