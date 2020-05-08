---
title: ピン データ範囲の指定
description: ピン データ範囲の指定
ms.assetid: bef74cd1-d2be-402d-be7f-acc7d8cbf392
keywords:
- WDK オーディオ、データ範囲をピン留めする
- WDM オーディオドライバー WDK、ピンデータ範囲
- オーディオドライバー WDK、ピン留めデータ範囲
- データ範囲 WDK オーディオ、pin
- 構成可能な pin WDK オーディオドライバー
- WDK オーディオ、pin データ範囲の形式を設定します
- WDK オーディオドライバーの共通部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 251ab44242d47cde57eb08ac81636b17e7ef746c
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925513"
---
# <a name="specifying-pin-data-ranges"></a>ピン データ範囲の指定


デバイスのデータパスと制御ノードを表すトポロジを定義したら、次の手順として、構成可能な各 pin の[データ範囲](audio-data-ranges.md)を定義します。 構成可能な pin を作成して構成し、波形または MIDI ストリームに接続することができます。 これに対して、物理的な接続またはブリッジピンは暗黙的に存在するため、ソフトウェア制御で作成または構成することはできません。

Wave または MIDI ストリームのシンクまたはソースとして機能するように構成可能な pin を接続する前に、ストリームのデータ形式を処理するように pin を構成する必要があります。 通常、pin は、いくつかのストリーム形式のいずれかを受け入れるように構成できます。 たとえば、PCM の波出力ピンは、次の範囲の PCM ストリームパラメーターを受け取る場合があります。

-   11.025 kHz、22.05 kHz、44.1 kHz、および 48 kHz のサンプル料金

-   8、16、24、および32ビットのサンプルサイズ

-   1 ~ 8 の任意の数のチャネル

構成可能な pin の種類ごとに、ピン留めによって処理できるさまざまなストリームデータ形式がミニポートドライバーによって記述されます。 これらのパラメーター範囲は、次のコード例に示すように、データ範囲記述子の配列として指定できます。

```cpp
static KSDATARANGE_AUDIO PinDataRangesPcm[] =
{
    {
        {
            sizeof(KSDATARANGE_AUDIO),
            0,
            0,
            0,
            STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
            STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM),
            STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
        },
        8,       // Maximum number of channels
        8,       // Minimum number of bits-per-sample
        32,      // Maximum number of bits-per-channel
        11025,   // Minimum rate
        48000    // Maximum rate
    }
};
```

前の例`PinDataRangesPcm`の配列には、 [**ksk datarの\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)型の単一のデータ範囲記述子が含まれていることに注意してください。 一般に、データ範囲配列には任意の数の記述子を含めることができます。 たとえば、PCM 以外の wave 出力ピンでは、AC-3 over S/PDIF と WMA Pro over-S/PDIF 形式の両方がサポートされている場合があります。 これら2つの形式はそれぞれ、個別のデータ範囲記述子によって指定されます。 このため、pin のデータ範囲配列には、少なくとも2つの\_ksdatarange 構造体が含まれます。

DirectMusic を使用するアプリケーションの音楽ストリーム形式をサポートする構成可能な pin、または Windows マルチメディア midiIn*xxx*と Midiin*xxx*関数では、 [**ksk\_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)の型のデータ範囲記述子を使用します。

ポートドライバーは、ミニポートドライバーからデータ範囲情報を取得し、可能な限りこの情報を使用して、各 pin がサポートできるデータ形式に関する情報の要求を処理します。 単純な PCM データ範囲のピンの場合、ポートドライバーはその pin の共通部分要求を処理できます。 共通の要求では、クライアントは、ストリームに対して使用可能なデータ形式を表すデータ範囲のセットを提供します。 可能であれば、ポートドライバーの交差ハンドラーは、要求内のデータ範囲から特定のデータ形式を選択し、その pin のデータ範囲内にも含まれます。 この形式は、データ範囲の2つのセットの積集合を表します。 このため、クライアントと pin の両方でこの形式のストリームを処理できます。 より複雑なデータ範囲の場合、ミニポートドライバーは独自の共通部分ハンドラーを提供できます。これは、ポートドライバーが独自の既定のハンドラーの代わりに使用します。 ミニポートドライバーの共通部分ハンドラーを使用すると、データ範囲の配列としてポートドライバーを表現するのが困難な場合があります。 詳細については、「[データ共通ハンドラー](data-intersection-handlers.md) 」と「[複数チャネルオーディオデータと WAVE ファイル](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn653308(v=vs.85))」を参照してください。
