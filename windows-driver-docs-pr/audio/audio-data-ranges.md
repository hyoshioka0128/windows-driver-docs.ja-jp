---
title: オーディオ データ範囲
description: オーディオ データ範囲
ms.assetid: 690fafda-fb35-43da-9de1-6cbc3bf8eb6c
keywords:
- データ範囲の WDK オーディオ
- 範囲値の WDK オーディオ
- KS データ範囲の WDK オーディオ
- WDK のオーディオ データ範囲
- KSDATARANGE 構造体
- WDM オーディオ データ範囲 WDK
- オーディオ データの範囲について、データ範囲の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60eb376ca10b72d32f4ba01ff14e53dd2d01f7c3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355731"
---
# <a name="audio-data-ranges"></a>オーディオ データ範囲


## <span id="audio_data_ranges"></span><span id="AUDIO_DATA_RANGES"></span>


各ピン KS フィルターでは、データの形式がサポートを宣言します。 暗証番号 (pin) ファクトリでは、この情報は、データ範囲の配列として公開します。 前に説明した形式の記述子とは異なり、データ範囲はさまざまなデータ形式について説明します。 たとえば、wave 暗証番号 (pin) のデータ範囲には、サンプル サイズ、頻度、および、暗証番号 (pin) をサポートするチャネルの範囲を指定します。

ミニポート ドライバーには、pin がインスタンス化、ときに、暗証番号 (pin) のデータの範囲から選択する特定のデータ形式のストリームを処理するために pin を構成します。 この作業は、接続できるように 2 つの pin に共通するオーディオ データ形式を選択する、ミニポート ドライバーの交差部分のデータ ハンドラーによって行われます。 詳細については、次を参照してください。[交差部分のデータ ハンドラー](data-intersection-handlers.md)します。

プロパティの要求を使用して、データの範囲やデータの選択の交差部分をオーディオ ピンを照会する方法については、次を参照してください。[暗証番号 (pin) のデータ範囲は、プロパティの積集合](pin-data-range-and-intersection-properties.md)します。

Wave 暗証番号 (pin) のデータ範囲を指定する、 [ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体のサンプル サイズ、頻度、および、暗証番号 (pin) をサポートするチャネルの範囲を説明する情報が続きます。 KSDATARANGE 構造体そのものを含め、この情報にカプセル化、 [ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体。

MIDI または DirectMusic 暗証番号 (pin) のデータ範囲を指定するには、詳細については、チャネルと同時に再生できるノートの最大数を含む KSDATARANGE 構造が続きます。 KSDATARANGE 構造自体と共に、この情報にカプセル化、 [ **KSDATARANGE\_音楽**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_music)構造体。

このドキュメントでは、KSDATARANGE を使用するデータ範囲の例をいくつか\_オーディオおよび KSDATARANGE\_音楽構造体。

-   たとえば wave、DirectSound のデータ範囲の宣言を参照してください[PCM Stream データ範囲](pcm-stream-data-range.md)と[DirectSound Stream データ範囲](directsound-stream-data-range.md)します。

-   たとえば、MIDI、DirectMusic のデータ範囲の宣言を参照してください[MIDI Stream データ範囲](midi-stream-data-range.md)と[DirectMusic Stream データ範囲](directmusic-stream-data-range.md)します。

-   たとえば、PCM 以外の形式のデータ範囲の宣言を参照してください[ac-3 データ範囲を指定する](specifying-ac-3-data-ranges.md)と[WMA Pro データの範囲を指定する](specifying-wma-pro-data-ranges.md)します。

 

 




