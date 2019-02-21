---
title: WDM レガシ Windows マルチ メディア Api へのオーディオ拡張機能
description: WDM レガシ Windows マルチ メディア Api へのオーディオ拡張機能
ms.assetid: a1009b7f-3720-454f-a128-ae148f781edc
keywords:
- WDM オーディオ拡張 WDK
- WDK オーディオのオーディオ機能を拡張
- WDM オーディオ ドライバー WDK、拡張機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14860d7795db633e22ce113c4ad67738e86c7cb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560282"
---
# <a name="wdm-audio-extensions-to-legacy-windows-multimedia-apis"></a>WDM レガシ Windows マルチ メディア Api へのオーディオ拡張機能


## <span id="wdm_audio_extensions_to_legacy_windows_multimedia_apis"></span><span id="WDM_AUDIO_EXTENSIONS_TO_LEGACY_WINDOWS_MULTIMEDIA_APIS"></span>


最近のバージョンの Windows では、Windows マルチ メディア Api aux、midiIn、midiOut、ミキサー、waveIn、および状態と WDM オーディオ ドライバーの機能についての情報を出力する waveOut オーディオ機能を拡張してきました。

[ **AuxGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd756712)、 [ **midiInGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd798453)、 [ **midiOutGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd798469)、 [ **mixerGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd757300)、 [ **waveInGetDevCaps**](https://msdn.microsoft.com/library/windows/desktop/dd743841)、および[ **waveOutGetDevCaps** ](https://msdn.microsoft.com/library/windows/desktop/dd743857)関数は、オーディオ デバイスを一意に識別するドライバー固有の情報を取得できます。

Windows のマルチ メディア機能[ **waveInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743846)、 [ **waveOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743865)、 [ **midiInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798457)、 [ **midiOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798475)、および[ **mixerMessage** ](https://msdn.microsoft.com/library/windows/desktop/dd757307)を取得できますwave、MIDI、またはミキサーのデバイスのデバイスのインターフェイスの名前。 さらに、 **waveOutMessage**、 **midiOutMessage**、および**waveInMessage**関数がウェーブの I/O、MIDI、優先するオーディオ デバイスのデバイス Id を取得し、通信をそれぞれボイスです。

このセクションでは、次のトピックがについて説明します。

[WDM オーディオ ドライバーからの拡張機能](extended-capabilities-from-a-wdm-audio-driver.md)

[デバイスのシステム インターセプト メッセージ](system-intercepted-device-messages.md)

[好みのデバイス ID にアクセスします。](accessing-the-preferred-device-id.md)

[推奨される音声通信デバイス ID](preferred-voice-communications-device-id.md)

[デバイスのインターフェイス名を取得します。](obtaining-a-device-interface-name.md)

[音楽テクノロジの Guid](music-technology-guids.md)

 

 




