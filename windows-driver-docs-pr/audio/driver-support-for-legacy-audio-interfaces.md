---
title: レガシ オーディオ インターフェイス用のドライバー サポート
description: レガシ オーディオ インターフェイス用のドライバー サポート
ms.assetid: c1b81c58-de05-45e7-94ab-5d174d51dfd6
keywords:
- WDM オーディオ ドライバー WDK、レガシー インターフェイス
- オーディオ ドライバー WDK、レガシー インターフェイス
- 従来のインターフェイスをオーディオ WDK オーディオ
- インターフェイスの WDK オーディオ
- オーディオのミニポート ドライバー WDK、レガシー インターフェイス
- ミニポート ドライバー WDK オーディオ、レガシー インターフェイス
- Windows のマルチ メディア サポート WDK オーディオ
- WDK のマルチ メディア オーディオ
- ミニポート インターフェイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19855d6fcb8bbfd7f99248e87689f87639fce4dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580369"
---
# <a name="driver-support-for-legacy-audio-interfaces"></a>レガシ オーディオ インターフェイス用のドライバー サポート


## <span id="driver_support_for_legacy_audio_interfaces"></span><span id="DRIVER_SUPPORT_FOR_LEGACY_AUDIO_INTERFACES"></span>


WDM のオーディオ システムでは、従来の Windows のマルチ メディア関数を使用してオーディオ デバイスにアクセスするアプリケーション プログラムのドライバーのサポートを提供します。 これらの機能には、次のオーディオ固有の Api があります。

-   Aux

-   Mixer

-   midiIn

-   midiOut

-   wavein クラス

-   waveOut

これらの Api については、Microsoft Windows SDK のドキュメントを参照してください。 従来のオーディオ機能のドライバーのサポートを提供するシステム コンポーネントの説明は、[WDM オーディオ コンポーネント](wdm-audio-components.md)を参照してください。

このセクションでは、オーディオ ミニポート ドライバー サポートを強化するアプリケーション プログラムを Windows のマルチ メディア機能を公開するオーディオ機能との実装のできる機能について説明します。 これらの機能には、wave stream キャプチャし、レンダリング、MIDI 記録、合成とミキサー コントロールが含まれます。 さらに、このセクションでは、ドライバー固有のオーディオ デバイス情報を取得するアプリケーションが使用できる、従来のオーディオ固有 Api をいくつかの拡張機能について説明します。

このセクションでは、次のトピックについて説明します。

[カーネル ストリーム オーディオ Mixer API への変換からのトポロジ](kernel-streaming-topology-to-audio-mixer-api-translation.md)

[WDM レガシ Windows マルチ メディア Api へのオーディオ拡張機能](wdm-audio-extensions-to-legacy-windows-multimedia-apis.md)

 

 




