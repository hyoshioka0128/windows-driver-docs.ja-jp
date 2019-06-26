---
title: レガシ Windows マルチ メディア API に対する WDM オーディオの拡張機能
description: レガシ Windows マルチ メディア API に対する WDM オーディオの拡張機能
ms.assetid: a1009b7f-3720-454f-a128-ae148f781edc
keywords:
- WDM オーディオ拡張 WDK
- WDK オーディオのオーディオ機能を拡張
- WDM オーディオ ドライバー WDK、拡張機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186c5cb6efd3921128dee681bb94520e69fa3606
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354103"
---
# <a name="wdm-audio-extensions-to-legacy-windows-multimedia-apis"></a>レガシ Windows マルチ メディア API に対する WDM オーディオの拡張機能


## <span id="wdm_audio_extensions_to_legacy_windows_multimedia_apis"></span><span id="WDM_AUDIO_EXTENSIONS_TO_LEGACY_WINDOWS_MULTIMEDIA_APIS"></span>


最近のバージョンの Windows では、Windows マルチ メディア Api aux、midiIn、midiOut、ミキサー、waveIn、および状態と WDM オーディオ ドライバーの機能についての情報を出力する waveOut オーディオ機能を拡張してきました。

[ **AuxGetDevCaps**](https://docs.microsoft.com/previous-versions/dd756712(v=vs.85))、 [ **midiInGetDevCaps**](https://docs.microsoft.com/previous-versions/dd798453(v=vs.85))、 [ **midiOutGetDevCaps**](https://docs.microsoft.com/previous-versions/dd798469(v=vs.85))、 [ **mixerGetDevCaps**](https://docs.microsoft.com/previous-versions/dd757300(v=vs.85))、 [ **waveInGetDevCaps**](https://docs.microsoft.com/previous-versions/dd743841(v=vs.85))、および[ **waveOutGetDevCaps** ](https://docs.microsoft.com/previous-versions/dd743857(v=vs.85))関数は、オーディオ デバイスを一意に識別するドライバー固有の情報を取得できます。

Windows のマルチ メディア機能[ **waveInMessage**](https://docs.microsoft.com/previous-versions/dd743846(v=vs.85))、 [ **waveOutMessage**](https://docs.microsoft.com/previous-versions/dd743865(v=vs.85))、 [ **midiInMessage**](https://docs.microsoft.com/previous-versions/dd798457(v=vs.85))、 [ **midiOutMessage**](https://docs.microsoft.com/previous-versions/dd798475(v=vs.85))、および[ **mixerMessage** ](https://docs.microsoft.com/previous-versions/dd757307(v=vs.85))を取得できますwave、MIDI、またはミキサーのデバイスのデバイスのインターフェイスの名前。 さらに、 **waveOutMessage**、 **midiOutMessage**、および**waveInMessage**関数がウェーブの I/O、MIDI、優先するオーディオ デバイスのデバイス Id を取得し、通信をそれぞれボイスです。

このセクションでは、次のトピックがについて説明します。

[WDM オーディオ ドライバーからの拡張機能](extended-capabilities-from-a-wdm-audio-driver.md)

[デバイスのシステム インターセプト メッセージ](system-intercepted-device-messages.md)

[好みのデバイス ID にアクセスします。](accessing-the-preferred-device-id.md)

[推奨される音声通信デバイス ID](preferred-voice-communications-device-id.md)

[デバイスのインターフェイス名を取得します。](obtaining-a-device-interface-name.md)

[音楽テクノロジの Guid](music-technology-guids.md)

 

 




