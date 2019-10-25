---
title: オーディオ データ範囲
description: オーディオ データ範囲
ms.assetid: 690fafda-fb35-43da-9de1-6cbc3bf8eb6c
keywords:
- データ範囲 WDK オーディオ
- 範囲値 WDK オーディオ
- KS データ範囲 WDK オーディオ
- オーディオデータ範囲 WDK
- KSDATARANGE 構造体
- WDM オーディオデータ範囲 WDK
- データ範囲 WDK オーディオ、オーディオデータ範囲について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32dfe3d7465975568c5dc7f94ca92696c986191c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831404"
---
# <a name="audio-data-ranges"></a>オーディオ データ範囲


## <span id="audio_data_ranges"></span><span id="AUDIO_DATA_RANGES"></span>


KS フィルターの各ピンは、サポートするデータ形式を宣言します。 Pin ファクトリは、この情報をデータ範囲の配列として公開します。 前に説明した形式記述子とは異なり、データ範囲はデータ形式の範囲を記述します。 たとえば、wave pin のデータ範囲は、pin がサポートするサンプルサイズ、頻度、およびチャネルの範囲を指定します。

ミニポートドライバーによってピンがインスタンス化されると、pin のデータ範囲から選択された特定のデータ形式のストリームを処理するように pin が構成されます。 この作業は、ミニポートドライバーのデータの交差ハンドラーによって行われます。これにより、2つの pin に共通するオーディオデータ形式が選択され、接続できるようになります。 詳細については、「[データの交差ハンドラー](data-intersection-handlers.md)」を参照してください。

プロパティ要求を使用してデータ範囲のオーディオピンを照会し、データの交差部分を選択する方法の詳細については、「[データ範囲と交差プロパティのピン留め](pin-data-range-and-intersection-properties.md)」を参照してください。

Wave ピンのデータ範囲を指定するために、 [**Ksk datarの**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))構造体の後に、pin がサポートするサンプルサイズ、頻度、およびチャネルの範囲を説明する情報が続きます。 この情報 (KSDATARANGE 構造自体を含む) は、 [**Ksk datarの\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造にカプセル化されています。

MIDI または DirectMusic ピンのデータ範囲を指定するために、KSK DATARの構造体の後に、同時に再生できるチャネルとノートの最大数などの追加情報が続きます。 この情報は、KSDATARANGE 構造自体と共に、 [**ksdatarange\_ミュージック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)構造体にカプセル化されています。

このドキュメントでは、次のような\_のオーディオと KSK の\_のミュージック構造体を使用するデータ範囲の例をいくつか紹介します。

-   Wave データ範囲と DirectSound データ範囲の宣言の例については、「 [PCM ストリームデータ範囲](pcm-stream-data-range.md)」と「 [Directsound ストリームのデータ範囲](directsound-stream-data-range.md)」を参照してください。

-   MIDI と DirectMusic のデータ範囲の宣言の例については、「 [Midi ストリームのデータ範囲](midi-stream-data-range.md)」と「 [Directmusic ストリームのデータ範囲](directmusic-stream-data-range.md)」を参照してください。

-   PCM 以外の形式のデータ範囲の宣言の例については、「 [AC 3 データ範囲の指定](specifying-ac-3-data-ranges.md)」および「 [WMA Pro データ範囲の指定](specifying-wma-pro-data-ranges.md)」を参照してください。

 

 




