---
title: オーディオ データ形式
description: オーディオ データ形式
ms.assetid: e16c10ea-0193-4cf4-91a3-4f8d4a0d5cf6
keywords:
- データ形式の WDK オーディオ
- WDK のオーディオ、データを書式設定します。
- オーディオ データ形式 WDK
- wave ストリーム WDK オーディオ
- デジタル形式の WDK オーディオ
- ストリーム形式の WDK オーディオ
- KS データ形式の WDK オーディオ
- KSDATAFORMAT 構造体
- オーディオ データ形式の WDM WDK
- WDK のオーディオを形式します。
- データ形式のオーディオ データ形式の詳細については、WDK オーディオ
ms.date: 02/15/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f6d9fff6d993d9fba7a671ec41f014d9d6391b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355734"
---
# <a name="audio-data-formats"></a>オーディオ データ形式


## <span id="audio_data_formats"></span><span id="AUDIO_DATA_FORMATS"></span>


Wave オーディオ ストリームのデータ形式を指定する、 [ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)構造がいずれかですぐにその後に、 [ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)または[ **KSDSOUND\_BUFFERDESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdsound_bufferdesc)構造体、および**指定子**KSDATAFORMAT のメンバーは、次のいずれかに設定に応じて2 つの値。

-   KSDATAFORMAT\_指定子\_WAVEFORMATEX

    Wave ストリーム、waveIn または waveOut アプリケーションによって使用されているデータ形式が属していることを示します。 この場合は場合、KSDATAFORMAT 構造体の*FormatSize*十分では、次のデータ形式指定子 KSDATAFORMAT 構造は WAVEFORMATEX 構造。

-   KSDATAFORMAT\_指定子\_DSOUND

    DirectSound アプリケーションによって使用されている wave ストリームにデータ形式が属していることを示します。 ここでは、KSDATAFORMAT 構造を次のデータ形式指定子を KSDSOUND\_BUFFERDESC 構造体、WAVEFORMATEX 埋め込み構造体が含まれています。

[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造 KSDATAFORMAT 構造とそれに続く WAVEFORMATEX 構造の両方をカプセル化します。 同様に、 [ **KSDATAFORMAT\_DSOUND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_dsound)構造 KSDATAFORMAT 構造と、DSOUND の両方をカプセル化\_それに続く BUFFERDESC 構造体。

いずれかの KSDATAFORMAT\_WAVEFORMATEX または KSDATAFORMAT\_DSOUND、構造体の最後の項目は、埋め込み WAVEFORMATEX 構造体; KSDATAFORMAT 場合\_DSOUND、WAVEFORMATEX 構造に含まれている、埋め込み DSOUND\_BUFFERDESC 構造体。 先頭にある可能性がありますいずれの場合も、WAVEFORMATEX 構造、 [ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)構造体の場合、 **wFormatTag** WAVEFORMATEX のメンバーの設定WAVE 値に\_形式\_拡張可能です。 詳細については、次を参照してください。 [Wave 形式の拡張可能な記述子](extensible-wave-format-descriptors.md)します。

MIDI ストリームまたは DirectMusic ストリームのデータ形式を指定するには KSDATAFORMAT 構造で十分です。その他の情報に続くされません。

Wave と DirectSound データ形式の例については、次を参照してください。 [PCM Stream データ形式](pcm-stream-data-format.md)と[DirectSound Stream データ形式](directsound-stream-data-format.md)します。 MIDI と DirectMusic データ形式の例については、次を参照してください。 [MIDI Stream データ形式](midi-stream-data-format.md)と[DirectMusic Stream データ形式](directmusic-stream-data-format.md)します。

 

 




