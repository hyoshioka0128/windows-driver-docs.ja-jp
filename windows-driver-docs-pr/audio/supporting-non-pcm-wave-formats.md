---
title: PCM 以外の Wave 形式のサポート
description: PCM 以外の Wave 形式のサポート
ms.assetid: 76455e1f-4b00-49c4-a4e4-3cb4abe8f445
keywords:
- 非 PCM オーディオ形式 WDK
- WDM オーディオ ドライバー WDK、wave 形式の非 PCM
- オーディオ ドライバー WDK、wave 形式の非 PCM
- WDK オーディオ、非 PCM を書式設定します。
- PCM の形式の WDK オーディオ
- PCM 以外のオーディオ形式 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f514fabe610acf94764ad6cce38869fb92bd85e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328557"
---
# <a name="supporting-non-pcm-wave-formats"></a>PCM 以外の Wave 形式のサポート


## <span id="supporting_non_pcm_wave_formats"></span><span id="SUPPORTING_NON_PCM_WAVE_FORMATS"></span>

このセクションでは、クライアントが非 PCM のオーディオを再生できないし、一連のより新しいバージョンの Windows で PCM 以外のデータ形式をサポートする WDM オーディオ ドライバーを適合させるためのガイドラインを提示する Windows の以前のバージョンの制限事項について説明します。

さらに、このセクションでは、新しいサブフォーマット圧縮オーディオ形式のサポートを提供する Windows 7 での Guid をについて説明します。

ここでは、次のトピックについて説明します。

[PCM 以外のサポートの背景](background-of-non-pcm-support.md)

[非 PCM のピン留めするファクトリの要件](requirements-for-a-non-pcm-pin-factory.md)

[圧縮されたオーディオ形式のサブフォーマット Guid](subformat-guids-for-compressed-audio-formats.md)

[形式のタグとサブフォーマット Guid 間の変換](converting-between-format-tags-and-subformat-guids.md)

[KS トポロジに関する考慮事項](ks-topology-considerations.md)

[WaveOut クライアントの詳細](specifics-for-waveout-clients.md)

[DirectSound クライアントの詳細](specifics-for-directsound-clients.md)

[S/PDIF パススルー送信 PCM されたストリーム](s-pdif-pass-through-transmission-of-non-pcm-streams.md)

[Ac-3 データ範囲を指定します。](specifying-ac-3-data-ranges.md)

[WMA Pro データ範囲を指定します。](specifying-wma-pro-data-ranges.md)

[PCM 以外の形式の USB オーディオ サポート](usb-audio-support-for-non-pcm-formats.md)


 

 




