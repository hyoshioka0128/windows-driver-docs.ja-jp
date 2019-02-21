---
title: 暗証番号 (pin) のデータ範囲を指定します。
description: 暗証番号 (pin) のデータ範囲を指定します。
ms.assetid: bef74cd1-d2be-402d-be7f-acc7d8cbf392
keywords:
- WDK のオーディオ、データの範囲をピン留め
- WDM オーディオ ドライバー WDK、データの範囲をピン留めします。
- オーディオ ドライバー WDK、データの範囲をピン留めします。
- データの範囲は、オーディオ ピンを WDK
- 構成可能なピン WDK オーディオ ドライバー
- WDK のオーディオ、暗証番号 (pin) のデータ範囲の書式設定します。
- WDK のオーディオ ドライバーの交差部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 079a7f348257d6aa9f6c77d1e940d8f94efdd389
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528731"
---
# <a name="specifying-pin-data-ranges"></a>暗証番号 (pin) のデータ範囲を指定します。


データ パスを表し、デバイス内のノードを制御するトポロジを定義した後、次の手順が定義には、[データ範囲](audio-data-ranges.md)構成可能な各ピンにします。 構成可能な暗証番号 (pin) の作成、構成、および wave またはソフトウェアの管理下にある MIDI ストリームに接続されていることができます。 これに対し、物理接続またはブリッジのピン留めが暗黙的に存在することができ、どちらもする作成ソフトウェア制御の下で構成します。

Wave または MIDI ストリームのソースまたはシンクとして機能する構成可能な暗証番号 (pin) を接続する前に、ストリームのデータ形式を処理するために、暗証番号 (pin) を構成する必要があります。 通常、stream の形式をいくつかのいずれかを受け入れるように、暗証番号 (pin) を構成できます。 たとえば、PCM wave 出力ピン留めは、PCM のストリームのパラメーターの次の範囲を受け付ける場合があります。

-   11.025 kHz、22.05 kHz、44.1 kHz、48 kHz のサンプル レート

-   8、16、24、および 32 ビットのサンプル サイズ

-   1 から 8 までのチャネルの任意の数

構成可能な暗証番号 (pin) の種類ごとに、ミニポート ドライバーには、暗証番号 (pin) を処理できるさまざまなストリームのデータ形式について説明します。 これらのパラメーターの範囲は、次のコード例に示すように、データ範囲の記述子の配列として指定できます。

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

なお、`PinDataRangesPcm`前の例では配列には型の 1 つのデータ範囲の記述子が含まれています[ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)します。 一般的には、データ範囲の配列は、任意の数の記述子を含めることができます。 たとえば、非 PCM wave 出力ピンには、AC-3-フェールオーバー-S/PDIF と WMA Pro オーバー-S/PDIF 形式の両方をサポート可能性があります。 これら 2 つの形式のそれぞれは、別のデータ範囲記述子によって指定されます。 したがって、暗証番号 (pin) のデータ範囲の配列が少なくとも 2 つの KSDATARANGE には含まれます\_オーディオ構造体。

DirectMusic または Windows のマルチ メディア midiIn を使用するアプリケーションからの音楽ファイル ストリームの形式をサポートする構成可能な pin*Xxx*と midiOut*Xxx*関数型のデータ範囲の記述子を使用します。[ **KSDATARANGE\_音楽**](https://msdn.microsoft.com/library/windows/hardware/ff537097)します。

ポート ドライバーでは、ミニポート ドライバーからデータ範囲情報を取得し、可能な限り、各暗証番号 (pin) をサポートするデータ形式に関する情報の要求を処理するために、この情報を使用します。 暗証番号 (pin) に単純な PCM データ範囲は、の場合は、ポート ドライバーはその暗証番号 (pin) の積集合の要求を処理できません。 積集合の要求では、クライアントは、ストリームの可能なデータ形式を表すデータ範囲のセットを提供します。 可能であれば、ポート ドライバーの積集合のハンドラーは、また、pin のデータの範囲内にある要求でデータの範囲から特定のデータ形式を取得します。 この形式は、2 つのデータ範囲のセットの積集合を表します。 そのため、クライアントと、暗証番号 (pin) の両方では、この形式のストリームを処理できます。 複雑なデータ範囲、ミニポート ドライバーは、独自の既定のハンドラーではなくポート ドライバーを使用して、独自の積集合ハンドラーを提供できます。 ミニポート ドライバーの積集合のハンドラーは、データ範囲の配列としてポート ドライバーに表現する困難な可能性のある形式の要件を許可できます。 詳細については、次を参照してください。[交差部分のデータ ハンドラー](data-intersection-handlers.md)します。 追加情報は、ホワイト ペーパーで使用できる*複数チャネルのオーディオ データ ファイルと WAVE ファイル*で、[オーディオ テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8751)web サイト。

 

 




