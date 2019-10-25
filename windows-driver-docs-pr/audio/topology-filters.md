---
title: トポロジ フィルター
description: トポロジ フィルター
ms.assetid: 1b3d35e9-5858-407c-9cd0-06307d82ce58
keywords:
- オーディオフィルター WDK オーディオ、トポロジフィルター
- トポロジフィルター WDK オーディオ
- WDK オーディオ、トポロジをフィルター処理します
- レンダリングストリームの混合 WDK オーディオ
- キャプチャストリームの多重化 WDK オーディオ
- ブリッジピン WDK オーディオ
- WDK オーディオの接続
- ファクトリ WDK オーディオをフィルター処理する
- WDK オーディオ、トポロジフィルターをピン留めする
- ノード WDK オーディオ
- 入力ピン WDK オーディオ
- 出力ピン WDK オーディオ
- PCCONNECTION_DESCRIPTOR 配列
- オーディオジャック WDK
- デジタルコネクタ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d860aa8c23be7e5670322a4652420dfa7f517da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830001"
---
# <a name="topology-filters"></a>トポロジ フィルター


## <span id="topology_filters"></span><span id="TOPOLOGY_FILTERS"></span>


*トポロジフィルター*は、カードで管理されているさまざまな wave ストリームと MIDI ストリームの間の相互作用を処理するオーディオアダプターカード上の回路の部分を表します。 この回路では、レンダリングストリームとキャプチャストリームの多重化が混在しています。

トポロジフィルターは、外部デバイスへのオーディオアダプターの物理的な接続を表す*ブリッジピン*(「[オーディオフィルターグラフ](audio-filter-graphs.md)」を参照) を提供します。 これらの接続には、通常、スピーカーやマイクからのアナログ入力信号を駆動するアナログ出力信号が付属しています。 トポロジフィルターのブリッジピンは、アナログの linein ジャックや lineout ジャック、場合によってはデジタル入出力コネクタも表すことができます。

"トポロジフィルター" という用語は、1つの意味で名称ます。 名前にかかわらず、トポロジフィルターは、内部トポロジまたはレイアウトを公開する、いくつかの種類のオーディオフィルターの1つにすぎません。 トポロジフィルターには主要なトポロジ機能が含まれていますが、アダプター全体のトポロジが必ずしも含まれるとは限りません。 Wave フィルターと MIDI フィルターには、独自のトポロジがあります。 たとえば、最小の WaveCyclic または WavePci フィルター (「 [Wave フィルター](wave-filters.md)」を参照) は、基になるデバイスが使用しているかどうかに応じて、2つのピンと DAC (デジタル-アナログコンバーター) または ADC (アナログ-デジタルコンバーター) で構成されるトポロジを公開する可能性があります。オーディオレンダリングまたはキャプチャ。

トポロジフィルターは、ポートとミニポートのペアとして実装されます。 トポロジフィルターファクトリは、次のようにトポロジフィルターを作成します。

-   トポロジミニポートドライバーオブジェクトをインスタンス化します。

-   このメソッドは、GUID 値**CLSID\_PortTopology**を持つ[**pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出すことによって、トポロジポートドライバーオブジェクトをインスタンス化します。

-   ポートドライバーの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出して、ミニポートドライバーをポートドライバーにバインドします。

[サブデバイス作成](subdevice-creation.md)のコード例では、このプロセスを示しています。

トポロジポートとミニポートドライバーは、それぞれの[Iporttopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)インターフェイスと[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)インターフェイスを介して相互に通信します。 これらのインターフェイスは、ピンを通過するストリームをトポロジフィルターが明示的に管理する必要がないため、wave および MIDI ポートおよびミニポートドライバーのインターフェイスと比べて比較的単純です。 トポロジフィルターのピンは、アダプターハードウェアでの配線された接続を表します。 トポロジフィルターピンの基になる物理接続には、通常、アナログオーディオ信号が適用されますが、ハードウェアの実装によっては、代わりにデジタルオーディオストリームが適用される場合があります。

[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)、 [IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)、 [IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)、 [IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)の各インターフェイスとは対照的に、 [IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)インターフェイスに**newstream**メソッドはありません。

トポロジフィルターの機能のほとんどは、そのプロパティハンドラーによって提供されます。 トポロジフィルターは主に、 [Sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)および Microsoft Windows マルチメディアミキサー API を使用するアプリケーションにトポロジ情報を提供するために存在します。 トポロジフィルターのプロパティハンドラーは、オーディオアダプターが通常提供するさまざまなコントロール (ボリューム、イコライゼーション、リバーブなど) へのアクセスを提供します。 ミキサ API は、プロパティ要求を使用して、アダプターハードウェア内の制御ノードの列挙、ノード間の接続の検出、およびノードのコントロールパラメーターの設定を行うことができます。 SndVol32 アプリケーション (「 [SysTray と SndVol32](systray-and-sndvol32.md)」を参照) では、ミキサー API を使用して、アダプターのストリームごとのボリュームとミュートの制御を検出します。

フィルターグラフを構築するときに、SysAudio は Ksk プロパティのトポロジフィルターを照会し、そのピンで[ **\_PHYSICALCONNECTION プロパティを\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)留めして、どのような電波、MIDI、または DirectMusic フィルターピンがどのトポロジフィルターピンに接続されているかを判断します。

Wave、MIDI、または DirectMusic フィルターとは異なり、トポロジフィルターではピンがインスタンス化されません。 したがって、トポロジフィルターの pin プロパティに対するクエリを処理するために使用できるピンオブジェクトはありません。 トポロジフィルター自体は、そのピンでの物理接続に関するすべてのクエリを処理します。 詳細については、「 [Ksk Propsetid\_Pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)」を参照してください。

他の種類のオーディオフィルターと同様に、トポロジフィルターは[**Pcconnection\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))構造体の配列を使用して内部トポロジを記述します。 ミニポートドライバーは、 [**IMiniport:: GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)メソッドから出力する[**PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)構造体でこの配列を公開します。 この配列は、トポロジフィルターのノードと pin の間の接続の一覧としてトポロジを指定します (「[ノードと接続](nodes-and-connections.md)」を参照してください)。 [WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)は、これらの接続とノードを、ミキサー API がアプリケーションに公開するミキサーの線とコントロールに変換します。 「[オーディオフィルター](audio-filters.md)」で説明されているように、KS フィルターの入力ピンは SRC ミキサ線にマップされ、フィルターの出力ピンは DST ミキサーラインにマップされます。

一般的なオーディオアダプターは、スピーカーを介して wave および MIDI ファイルを再生し、マイクと MIDI シンセサイザーからオーディオ信号をキャプチャできます。 次のコード例には、これらの機能を公開するトポロジフィルターの PCCONNECTION\_記述子配列が含まれています。

```cpp
    // topology pins
    enum
    {
        KSPIN_TOPO_WAVEOUT_SRC = 0,
        KSPIN_TOPO_SYNTHOUT_SRC,
        KSPIN_TOPO_SYNTHIN_SRC,
        KSPIN_TOPO_MIC_SRC,
        KSPIN_TOPO_LINEOUT_DST,
        KSPIN_TOPO_WAVEIN_DST
    };
 
    // topology nodes
    enum
    {
        KSNODE_TOPO_WAVEOUT_VOLUME = 0,
        KSNODE_TOPO_WAVEOUT_MUTE,
        KSNODE_TOPO_SYNTHOUT_VOLUME,
        KSNODE_TOPO_SYNTHOUT_MUTE,
        KSNODE_TOPO_MIC_VOLUME,
        KSNODE_TOPO_SYNTHIN_VOLUME,
        KSNODE_TOPO_LINEOUT_MIX,
        KSNODE_TOPO_LINEOUT_VOLUME,
        KSNODE_TOPO_WAVEIN_MUX
    };
 
    static PCCONNECTION_DESCRIPTOR MiniportConnections[] =
    {
       // FromNode---------------------FromPin------------------ToNode-----------------------ToPin
 
        { PCFILTER_NODE,               KSPIN_TOPO_WAVEOUT_SRC,  KSNODE_TOPO_WAVEOUT_VOLUME,  1 },
        { KSNODE_TOPO_WAVEOUT_VOLUME,  0,                       KSNODE_TOPO_WAVEOUT_MUTE,    1 },
        { KSNODE_TOPO_WAVEOUT_MUTE,    0,                       KSNODE_TOPO_LINEOUT_MIX,     1 },
 
        { PCFILTER_NODE,               KSPIN_TOPO_SYNTHOUT_SRC, KSNODE_TOPO_SYNTHOUT_VOLUME, 1 },
        { KSNODE_TOPO_SYNTHOUT_VOLUME, 0,                       KSNODE_TOPO_SYNTHOUT_MUTE,   1 },
        { KSNODE_TOPO_SYNTHOUT_MUTE,   0,                       KSNODE_TOPO_LINEOUT_MIX,     2 },
 
        { PCFILTER_NODE,               KSPIN_TOPO_SYNTHIN_SRC,  KSNODE_TOPO_SYNTHIN_VOLUME,  1 },
        { KSNODE_TOPO_SYNTHIN_VOLUME,  0,                       KSNODE_TOPO_WAVEIN_MUX,      1 },
 
        { PCFILTER_NODE,               KSPIN_TOPO_MIC_SRC,      KSNODE_TOPO_MIC_VOLUME,      1 },
        { KSNODE_TOPO_MIC_VOLUME,      0,                       KSNODE_TOPO_WAVEIN_MUX,      2 },
 
        { KSNODE_TOPO_LINEOUT_MIX,     0,                       KSNODE_TOPO_LINEOUT_VOLUME,  1 },
        { KSNODE_TOPO_LINEOUT_VOLUME,  0,                 PCFILTER_NODE,  KSPIN_TOPO_LINEOUT_DST },
 
        { KSNODE_TOPO_WAVEIN_MUX,      0,                 PCFILTER_NODE,  KSPIN_TOPO_WAVEIN_DST }
    };
```

前のコード例の定数[**Pcfilter\_ノード**](https://docs.microsoft.com/previous-versions/ff537695(v=vs.85))は、NULL ノード ID であり、ヘッダーファイル Portcls で定義されています。 この定数を使用して、フィルターの外部 pin とノードの論理ピンを区別する方法の詳細については、「 [**Pcconnection\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))」を参照してください。

前のコード例の各 pin 名は、ミキサー API がピンを変換元または変換先のミキサーラインにマップするかどうかによって、"SRC" または "DST" で終了します。 混乱を避けるために、ソースとターゲットのミキサーの線はそれぞれ、シンク (入力) と送信元 (出力) の各 KS フィルターのピンにマップされていることに注意してください。 詳細については、「[オーディオフィルター](audio-filters.md)」を参照してください。

前のコード例の PCCONNECTION\_記述子配列は、次の図のトポロジフィルターについて説明しています。

![pcconnection\-記述子配列によって記述されるトポロジフィルター接続を示す図](images/topofilt.png)

図のトポロジフィルターには、左側に4つの入力 (シンク) ピンがあり、右側に2つの出力 (ソース) ピンがあります。 上部の2つの入力ピンと上部の出力ピンを接続するデータパスは、再生されている wave ストリームと MIDI ストリームからレンダリングされた2つのアナログ信号をミックスします。 下部の2つの入力ピンおよび下部の出力ピンを接続するデータパスは、記録されているキャプチャされたアナログ信号を多重化します。

4つの入力ピンは次のように動作します。

-   KSPIN\_TOPO\_WAVEOUT\_SRC pin は、wave フィルターの出力ピンに物理的に接続されています。これにより、.wav ファイルなどのソースから wave ストリームがレンダリングされ、アナログ信号がピンで生成されます。

-   KSPIN\_TOPO\_SYNTHOUT\_SRC ピンは、シンセフィルターの出力ピンに物理的に接続されます。これは、たとえば、中間ファイルなどのソースからの MIDI ストリームを使用して、pin でアナログ信号を生成することがあります。

-   KSPIN\_TOPO\_SYNTHIN\_SRC ピンは、アナログ信号を生成するシンセサイザーに物理的に接続されています。 (実際のハードウェア設計では、MPU-401 MIDI インターフェイスから MIDI 入力ストリームを取得し、それを直接 wave 形式に変換して、トポロジフィルターを完全にバイパスすることに注意してください)。

-   KSPIN\_TOPO\_MIC\_SRC pin は、マイクからアナログ信号を受け取る入力ジャックに物理的に接続されています。

2つの出力ピンは次のように動作します。

-   KSPIN\_TOPO\_LINEOUT\_DST pin は、通常はスピーカーのセットをドライブするアナログ LINEOUT ジャックに物理的に接続されています。

-   KSPIN\_TOPO\_WAVEIN\_DST pin は、wave フィルターの入力ピンに物理的に接続されています。これにより、アナログ信号が wave ストリームに変換され、.wav ファイルなどの宛先に書き込まれます。

さまざまなストリームのボリュームレベルを制御するには、[ボリューム] ノードと [ミュート] ノード (「 [**KSNODETYPE\_volume**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume) and [**KSNODETYPE\_ミュート**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute)」を参照) を使用します。 SUM ノード (「 [**KSNODETYPE\_sum**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)」を参照) は、WAVE および MIDI 入力のオーディオストリームをミックスします。 MUX ノード (「 [**KSNODETYPE\_MUX**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux))」を参照して、2つの入力ストリームを選択します。

この図では、破線の矢印を使用して、2つのノード間またはピンとノードの間の接続を示しています。 矢印は、データフローの方向を指します。 図には合計13個の接続が示されています。各接続は、前のコード例の PCCONNECTION\_記述子配列内の13個の要素のいずれかに対応しています。

トポロジフィルターに加えて、アダプタードライバーでは、トポロジフィルターのピンに接続する他のフィルター (wave、FM シンセサイザー、wave テーブルなど) が作成されます。

たとえば、トポロジフィルターの KSPIN\_TOPO\_WAVEOUT\_SRC pin に物理的に接続されている wave フィルターには、PCM データをアナログ信号に変換する DAC ( [**KSNODETYPE\_DAC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)ノードによって表される) が含まれています。トポロジフィルターの pin に出力します。 Wavetable は、トポロジフィルターの KSPIN\_TOPO\_SYNTHOUT\_SRC pin に物理的に接続されている FM シンセサイザーまたはシンセサイザーフィルターと同様に、MIDI データを、トポロジフィルターの pin に出力するアナログ信号に変換します。 トポロジフィルターでは、これら2つの pin からのアナログ信号をミキシングし、混合信号をスピーカーに出力します。

トポロジフィルターでは、同じアダプターカードにある他のハードウェアデバイスを表す他のフィルターへの物理接続を、フィルターに対する他の種類の接続と区別する必要があります。 たとえば、wave、MIDI、および DirectMusic フィルターの特定のピンは、ソフトウェアコントロールで接続したり切断したりすることができます。

デバイスの起動時に、アダプタードライバーは、接続ごとに1回の[**Pcregiphysicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)を呼び出して、トポロジフィルターの物理接続を登録します。 ポートドライバーは、 [ **\_PHYSICALCONNECTION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)の get プロパティ要求を\_に、ksk プロパティに応答するためにこの情報を必要とします。

 

 




