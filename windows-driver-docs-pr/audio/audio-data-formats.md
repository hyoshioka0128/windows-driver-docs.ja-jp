---
title: オーディオ データ形式
description: オーディオ データ形式
ms.assetid: e16c10ea-0193-4cf4-91a3-4f8d4a0d5cf6
keywords:
- データ形式 WDK オーディオ
- WDK オーディオ、データをフォーマットします
- WDK のオーディオデータ形式
- wave ストリーム WDK オーディオ
- デジタル形式 WDK オーディオ
- WDK オーディオのストリーム形式
- KS データ形式 WDK オーディオ
- KSDATAFORMAT 構造体
- WDM オーディオデータ形式 WDK
- WDK オーディオをフォーマットします
- データ形式 WDK オーディオ、オーディオデータ形式について
ms.date: 02/15/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff9d0612bcd7149b8c0159ce25d3c547107bd452
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831909"
---
# <a name="audio-data-formats"></a>オーディオ データ形式


## <span id="audio_data_formats"></span><span id="AUDIO_DATA_FORMATS"></span>


Wave オーディオストリームのデータ形式を指定するには、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体の直後に[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)または[**KSDSOUND\_bufferdesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdsound_bufferdesc)構造体を指定します。 KSDATAFORMAT の**指定子**メンバーはです。それに応じて、次の2つの値のいずれかに設定されます。

-   KSDATAFORMAT\_指定子\_WAVEFORMATEX

    WaveIn または waveOut アプリケーションによって使用されている wave ストリームにデータ形式が属していることを示します。 この場合、KSDATAFORMAT 構造体の*Formatsize*が十分な大きさであれば、KSDATAFORMAT 構造体の後のデータ形式指定子は WAVEFORMATEX 構造体になります。

-   KSDATAFORMAT\_指定子\_DSOUND

    DirectSound アプリケーションによって使用されている wave ストリームにデータ形式が属していることを示します。 この場合、KSDATAFORMAT 構造体の後のデータ形式指定子は、埋め込み WAVEFORMATEX 構造体を含む KSDSOUND\_BUFFERDESC 構造体です。

[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体は、KSDATAFORMAT 構造体とそれに続く WAVEFORMATEX 構造体の両方をカプセル化します。 同様に、 [**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)構造体は、KSDATAFORMAT 構造体と、それに続く DSOUND\_bufferdesc 構造体の両方をカプセル化します。

KSDATAFORMAT\_WAVEFORMATEX または KSDATAFORMAT\_DSOUND では、構造体の最後の項目は埋め込みの WAVEFORMATEX 構造体です。KSDATAFORMAT\_DSOUND の場合、WAVEFORMATEX 構造体は、埋め込みの DSOUND\_BUFFERDESC 構造体に含まれています。 どちらの場合も、WAVEFORMATEX 構造体は[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体の先頭になることがあります。この場合、WAVEFORMATEX の**wFormatTag**メンバーは、値の WAVE\_形式\_拡張可能に設定されます。 詳細については、「[拡張 Wave 形式記述子](extensible-wave-format-descriptors.md)」を参照してください。

MIDI ストリームまたは DirectMusic ストリームのデータ形式を指定するには、KSDATAFORMAT 構造体で十分です。その後に追加情報はありません。

Wave および DirectSound データ形式の例については、「 [PCM ストリームデータ形式](pcm-stream-data-format.md)」と「 [Directsound ストリームのデータ形式](directsound-stream-data-format.md)」を参照してください。 MIDI と DirectMusic のデータ形式の例については、「 [Midi ストリームのデータ](midi-stream-data-format.md)形式」と「 [Directmusic ストリームのデータ形式](directmusic-stream-data-format.md)」を参照してください。

 

 




