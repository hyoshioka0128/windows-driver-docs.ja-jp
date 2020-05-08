---
title: PCM 以外の形式用の USB オーディオのサポート
description: PCM 以外の形式用の USB オーディオのサポート
ms.assetid: e4479a67-ec45-45f1-9c42-f050cb0f2eb2
keywords:
- USBAudio クラスシステムドライバー WDK オーディオ
- PCM 以外のオーディオ形式 WDK、USBAudio
- raw AC-3 WDK オーディオ
- AC 3 WDK オーディオ
- PCM 以外のオーディオ形式 WDK、AC-3
- USB オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca00c33b73d894e83342460ccce9154ef5d6e997
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925519"
---
# <a name="usb-audio-support-for-non-pcm-formats"></a>PCM 以外の形式用の USB オーディオのサポート


## <span id="usb_audio_support_for_non_pcm_formats"></span><span id="USB_AUDIO_SUPPORT_FOR_NON_PCM_FORMATS"></span>


Microsoft の[usbaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)である usbaudio は、現在、AC-3 が埋め込まれた USB オーディオタイプ III 形式をサポートしていません。 詳細については、 [USB 実装者フォーラム](https://www.usb.org/)の web サイトで、*オーディオデータ形式のユニバーサルシリアルバスデバイスクラス定義*に関する説明を参照してください。

USBAudio は、PortCls ドライバーによって受け付けられる、埋め込み、AC 3 over S/PDIF 形式ではなく、"未加工" の AC 3 パックを受け入れることができます。 USBAudio は、DirectShow の DVD スプリッターフィルターの内部形式をサポートしています (「 [Windows での Dvd デコーダーのサポート](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-decoder-support-in-windows)」を参照してください)。これは、ksk プロキシの制御下にある usbaudio に直接接続できます (「[カーネルストリーミングプロキシ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)」を参照してください)。 特に、USBAudio によって公開されている非埋め込み\_の\_AC\_3 データ範囲は KSDATAFORMAT SUBTYPE AC3 AUDIO です。これは\_、\_mediの種類 DOLBY ac3 と同じ GUID 値です。

現在、USBAudio では、PCM 以外のオーディオデータの DirectSound 再生はサポートされていません。

 

 




