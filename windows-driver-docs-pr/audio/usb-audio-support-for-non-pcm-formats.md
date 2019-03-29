---
title: PCM 以外の形式用の USB オーディオのサポート
description: PCM 以外の形式用の USB オーディオのサポート
ms.assetid: e4479a67-ec45-45f1-9c42-f050cb0f2eb2
keywords:
- USBAudio クラス システム ドライバー WDK オーディオ
- 非 PCM オーディオの形式、WDK USBAudio
- 生の ac-3 WDK オーディオ
- Ac-3 WDK オーディオ
- 非 PCM オーディオの形式、WDK ac-3
- USB オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f338f58f3fb616eb454ebf7ba0632f526ede748
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578510"
---
# <a name="usb-audio-support-for-non-pcm-formats"></a>PCM 以外の形式用の USB オーディオのサポート


## <span id="usb_audio_support_for_non_pcm_formats"></span><span id="USB_AUDIO_SUPPORT_FOR_NON_PCM_FORMATS"></span>


Microsoft の[USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)Usbaudio.sys は現在埋め込み ac-3 で USB オーディオ型 III 形式をサポートしていません。 詳細については、次を参照してください。、*ユニバーサル シリアル バス デバイス クラス定義のデータの形式のオーディオの*仕様、 [USB Implementers Forum](https://go.microsoft.com/fwlink/p/?linkid=8780) web サイト。

USBAudio には、パックされた、「未加工」の ac-3 (PortCls ドライバーで受け入れられる埋め込まれる、AC-3-フェールオーバー-S/PDIF 形式) ではなくを受け入れることができます。 USBAudio DirectShow の DVD スプリッター フィルターの内部形式をサポートしています (を参照してください[Windows での DVD デコーダー サポート](https://msdn.microsoft.com/library/windows/hardware/ff558763))、USBAudio KsProxy の制御下に直接接続していることができます (を参照してください[カーネル ストリーミング プロキシ](https://msdn.microsoft.com/library/windows/hardware/ff560877)). 具体的には、USBAudio によって公開される nonpadded ac-3 データ範囲は、KSDATAFORMAT\_サブタイプ\_AC3\_MEDIASUBTYPE と同じ GUID 値には、オーディオ\_DOLBY\_AC3 します。

現在、USBAudio は非 PCM オーディオ データの DirectSound 再生をサポートしていません。

 

 




