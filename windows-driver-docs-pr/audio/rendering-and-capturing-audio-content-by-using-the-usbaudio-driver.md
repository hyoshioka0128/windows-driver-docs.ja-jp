---
title: USBAudio ドライバーを使用したオーディオ コンテンツのレンダリングとキャプチャ
description: USBAudio ドライバーを使用したオーディオ コンテンツのレンダリングとキャプチャ
ms.assetid: 92a6ad18-75ba-4382-a6d1-42f28133a158
keywords:
- USBAudio クラス システム ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41fbe4fc3a3688d89af2f3898732d45728d21908
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573485"
---
# <a name="rendering-and-capturing-audio-content-by-using-the-usbaudio-driver"></a>USBAudio ドライバーを使用したオーディオ コンテンツのレンダリングとキャプチャ


## <span id="ddk_rendering_and_capturing_audio_content_by_using_the_usbaudio_driver"></span><span id="DDK_RENDERING_AND_CAPTURING_AUDIO_CONTENT_BY_USING_THE_USBAUDIO_DRIVER"></span>


次に示します、 [USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)レンダリングし、オーディオ コンテンツをキャプチャするように構成します。 この図では、USBAudio ドライバーは、USB オーディオ デバイスで終端要素を表すための pin を売り払っています。 KMixer、WDMAud、DirectSound などのオーディオのコンポーネントは、出力ストリームを表示または入力ストリームをキャプチャするこれらのピンに接続します。

![レンダリングと usbaudio ドライバーを使用して、オーディオ コンテンツを取り込むことを示す図](images/usbaud.png)

Microsoft Windows Driver Model (WDM) 音声コンポーネントの説明については、次を参照してください。

[DirectSound システム コンポーネント](user-mode-wdm-audio-components.md#directsound_system_component)

[WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)

[SBEmul システム ドライバー](kernel-mode-wdm-audio-components.md#sbemul_system_driver)

[KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)

[Redbook システム ドライバー](kernel-mode-wdm-audio-components.md#redbook_system_driver)

[スプリッター システム ドライバー](kernel-mode-wdm-audio-components.md#splitter_system_driver)

[SWMidi システム ドライバー](kernel-mode-wdm-audio-components.md#swmidi_system_driver)

[DMusic システム ドライバー](kernel-mode-wdm-audio-components.md#dmusic_system_driver)

USBAudio ドライバーの上にあるフィルター グラフの詳細については、次を参照してください。

[レンダリングと Wave コンテンツをキャプチャします。](rendering-and-capturing-wave-content.md)

[レンダリングと MIDI コンテンツをキャプチャします。](rendering-and-capturing-midi-content.md)

 

 




