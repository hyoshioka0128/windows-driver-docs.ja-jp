---
title: トポロジ フィルター
description: トポロジ フィルター
ms.assetid: 1b3d35e9-5858-407c-9cd0-06307d82ce58
keywords:
- オーディオは、WDK のオーディオ、トポロジのフィルターをフィルター処理します。
- トポロジのフィルターの WDK オーディオ
- WDK のオーディオ、トポロジをフィルター処理します。
- ストリームの WDK オーディオのレンダリングを混在させる
- 多重化するストリーム WDK オーディオのキャプチャ
- ブリッジ ピン WDK オーディオ
- 接続の WDK オーディオ
- フィルター ファクトリ WDK オーディオ
- WDK のオーディオ、トポロジのフィルターをピン留め
- ノードの WDK オーディオ
- 入力ピン WDK オーディオ
- 出力ピンの WDK オーディオ
- PCCONNECTION_DESCRIPTOR 配列
- WDK のオーディオ ジャック
- デジタル コネクタ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9851047bb4543c196f8953ddb74adb03ab15dba9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574483"
---
# <a name="topology-filters"></a>トポロジ フィルター


## <span id="topology_filters"></span><span id="TOPOLOGY_FILTERS"></span>


A*トポロジ フィルター*さまざまな wave と、カード上で管理される MIDI ストリーム間の相互作用を処理するオーディオ アダプター カードの回路の部分を表します。 この回路はレンダリング ストリームが混在すると、キャプチャのストリームを多重化します。

トポロジのフィルターを提供します、*ピンをブリッジ*(を参照してください[オーディオ フィルター グラフ](audio-filter-graphs.md)) 外部デバイスにオーディオのアダプターの物理接続を表します。 通常、これらの接続は、スピーカーを駆動するアナログ出力信号とマイクからのアナログ入力信号を実行します。 トポロジ フィルターのブリッジのピンは、アナログのライン入力とライン出力ジャックを表す場合も、デジタル入力さらしとコネクタの出力を可能性があります。

「トポロジ フィルター」という用語は、名称を 1 つの意味では。 その名前にもかかわらずトポロジ フィルターとは、その内部のトポロジやレイアウトを公開するオーディオ フィルターのいくつかの型の 1 つだけです。 トポロジのフィルターには、キー トポロジの機能が含まれますが、必ずしもがない、アダプターのトポロジ全体。 Wave および MIDI フィルターは、独自のトポロジを持ちます。 たとえば、最小 WaveCyclic または WavePci フィルター (を参照してください[Wave フィルター](wave-filters.md)) かどうかに応じて、2 つの pin がおよび DAC (アナログ デジタル コンバーター) または ADC (アナログ/デジタル コンバーター) で構成されるトポロジを公開する可能性があります、基になるデバイスはオーディオ レンダリングまたはキャプチャします。

トポロジのフィルターは、ポート/ミニポート ペアとして実装されます。 トポロジ フィルター ファクトリは、次のようにトポロジ フィルターを作成します。

-   トポロジのミニポート ドライバー オブジェクトがインスタンス化します。

-   呼び出すことによって、トポロジ ポート ドライバー オブジェクトをインスタンス化[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)の GUID 値**CLSID\_PortTopology**します。

-   ポート ドライバーの呼び出す[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)ポート ドライバーに、ミニポート ドライバーをバインドするメソッド。

コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています。

トポロジのポートおよびミニポートのドライバーが、それぞれ経由の相互通信[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)と[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)インターフェイス。 これらのインターフェイスは、トポロジのフィルターは、自分の pin を通過するストリームを明示的に管理する必要はないために、wave と MIDI ポートおよびミニポートのドライバーに比べると比較的簡単です。 トポロジ フィルターのピンは、アダプターのハードウェアで有線接続を表します。 通常トポロジ フィルター暗証番号 (pin) を基になる物理接続は、アナログのオーディオ信号の伝送が、ハードウェアの実装によってデジタル オーディオ ストリームを代わりに、実行可能性があります。

異なり、 [IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)、 [IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)、 [IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)、および[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699) インターフェイス[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)インターフェイスを持たない**NewStream**メソッド。

トポロジのフィルターの機能のほとんどは、そのプロパティのハンドラーによって提供されます。 トポロジの情報を提供するには、主に、トポロジのフィルターが存在する、 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)と Microsoft Windows のマルチ メディア ミキサー API を使用するアプリケーションにします。 トポロジのフィルターのプロパティのハンドラーは、通常、オーディオのアダプターを提供するさまざまなコントロール (ボリューム、イコライゼーション リバーブなど) へのアクセスを提供します。 プロパティの要求を使用ミキサー API ことができます、アダプターのハードウェアでコントロールのノードを列挙、ノード間の接続の検出および両方クエリを実行し、ノードのコントロールのパラメーターを設定します。 SndVol32 アプリケーション (を参照してください[システム トレイと SndVol32](systray-and-sndvol32.md)) ミキサー API を使用して、アダプターのストリームごとのボリュームと、ミュート ボタン コントロールを検出します。

SysAudio のトポロジのフィルター処理するクエリ フィルター グラフを作成するときに、 [ **KSPROPERTY\_PIN\_PHYSICALCONNECTION** ](https://msdn.microsoft.com/library/windows/hardware/ff565205) wave、MIDI を判断するには、そのピンでのプロパティ、または DirectMusic フィルター暗証番号 (pin) がどのトポロジ フィルター ピンに接続されています。

Wave とは異なり、MIDI または DirectMusic がフィルター、フィルターをトポロジにピンがインスタンス化できません。 そのため、トポロジ フィルターの pin のプロパティのクエリを処理するの暗証番号 (pin) のオブジェクトはありません。 トポロジ フィルター自体では、そのピンに物理的な接続に関するすべてのクエリを処理します。 詳細については、[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)を参照してください。

その他の種類のオーディオ フィルターと同様に、トポロジのフィルターを使用して配列の[ **PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)内部のトポロジを記述する構造体。 ミニポート ドライバーでは、この配列を公開する、 [ **PCFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537694)から出力の構造、 [ **IMiniport::GetDescription**](https://msdn.microsoft.com/library/windows/hardware/ff536765)メソッド。 配列は、トポロジのフィルターのノードと pin の間の接続の一覧としてトポロジを指定します (を参照してください[ノードと接続](nodes-and-connections.md))。 [WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)ミキサーの線およびミキサー API をアプリケーションに公開するコントロールにこれらの接続とノードを変換します。 説明したよう[オーディオ フィルター](audio-filters.md)KS フィルターの入力ピンが SRC ミキサー行にマップし、上の出力ピン留め、フィルターが DST ミキサーの行にマップされます。

一般的なのオーディオ アダプターでは、wave とを通じて、講演者、MIDI ファイルを再生できるし、MIDI シンセサイザー マイクからオーディオ信号をキャプチャできます。 次のコード例は、PCCONNECTION を含む\_これらの機能を公開するトポロジ フィルター記述子の配列。

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

定数[ **PCFILTER\_ノード**](https://msdn.microsoft.com/library/windows/hardware/ff537695)上記のコード例が null のノード ID と Portcls.h のヘッダー ファイルで定義されます。 ノードの論理ピンから外部 pin では、フィルターを区別するためにこの定数を使用する方法については、[ **PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)を参照してください。

上記のコード例では、各暗証番号 (pin) 名は、ミキサー API が送信元または送信先ミキサーの行に、暗証番号 (pin) をマップするかどうかに応じて、"SRC"または"DST"のいずれかで終了します。 そのソースと宛先ミキサーに注意してください、混乱を避けるシンク (入力) とソース (出力) KS フィルターのピンのマッピングをそれぞれ行します。 詳細については、[オーディオ フィルター](audio-filters.md)を参照してください。

PCCONNECTION\_記述子の配列を上記のコード例では、次の図にトポロジのフィルターをについて説明します。

![pcconnection で説明されているトポロジ フィルターの接続を示す図\-記述子の配列](images/topofilt.png)

図にトポロジ フィルター左の 4 つの (シンク) の入力ピンには、および 2 つの出力ピンが右側の (ソース)。 最上位の 2 つの入力ピンと最上位の出力ピンを接続するデータ パスは、wave および再生中、MIDI ストリームから表示されている 2 つのアナログ信号を混在させます。 下部にある 2 つの入力ピンと下部にある出力ピンを接続するデータ パスでは、キャプチャされたアナログ信号が記録されているを多重化します。

4 つの入力ピンが次のように動作します。

-   KSPIN\_TOPO\_WAVEOUT\_SRC 暗証番号 (pin) がアナログ信号に pin を生成するために .wav ファイルなどのソースからのウェーブ ストリームを表示、波形のフィルターの出力ピンに物理的に接続されています。

-   KSPIN\_TOPO\_SYNTHOUT\_SRC 暗証番号 (pin) がストリームをレンダリング、たとえば、MIDI、暗証番号 (pin) では、アナログのシグナルを生成するために .mid ファイルなどのソースから、シンセサイザーのフィルターの出力ピンに物理的に接続されています。

-   KSPIN\_TOPO\_SYNTHIN\_SRC 暗証番号 (pin) がアナログ信号を生成するシンセサイザーに物理的に接続されています。 (より実際的なハードウェアの設計が片方 MIDI インターフェイスから MIDI 入力ストリームを取得し、トポロジ フィルターを完全にバイパス、wave 形式に直接変換する可能性がありますに注意してください)。

-   KSPIN\_TOPO\_MIC\_SRC 暗証番号 (pin) は、マイク アナログ信号を受け取る入力のジャックに物理的に接続します。

2 つの出力ピンが次のように動作します。

-   KSPIN\_TOPO\_ライン出力\_DST 暗証番号 (pin) が通常一組のスピーカーを駆動するアナログのライン出力ジャックに物理的に接続されています。

-   KSPIN\_TOPO\_WAVEIN\_DST 暗証番号 (pin) がアナログ信号を wave ストリームに変換し、.wav ファイルなどの変換先に書き込みます wave フィルターの入力ピンに物理的に接続されています。

ボリュームとミュート ノード (を参照してください[ **KSNODETYPE\_ボリューム**](https://msdn.microsoft.com/library/windows/hardware/ff537208)と[ **KSNODETYPE\_ミュート**](https://msdn.microsoft.com/library/windows/hardware/ff537178)) ために使用されますさまざまなストリームのボリューム レベルを制御します。 合計ノード (を参照してください[ **KSNODETYPE\_合計**](https://msdn.microsoft.com/library/windows/hardware/ff537196)) から、wave および MIDI 入力オーディオ ストリームが混在します。 MUX ノード (を参照してください[ **KSNODETYPE\_MUX**](https://msdn.microsoft.com/library/windows/hardware/ff537180)) の 2 つの入力ストリームを選択します。

図では、破線の矢印を使用して、2 つのノード間または pin とノード間の接続を示します。 矢印は、データ フローの方向を指し示します。 図は、PCCONNECTION で 13 個の要素のいずれかに対応するそれぞれの 13 の接続の合計を示しています。\_前のコード例では、記述子の配列。

だけでなく、トポロジのフィルターは、アダプター ドライバーは、その他のフィルター - wave、FM シンセサイザー、wave テーブル、およびようになって、トポロジのフィルターのピンに接続を作成します。

Wave フィルターなど、トポロジのフィルターの KSPIN に物理的に接続されている\_TOPO\_WAVEOUT\_SRC pin には、DAC が含まれています (によって表される、 [ **KSNODETYPE\_DAC**](https://msdn.microsoft.com/library/windows/hardware/ff537158)ノード) トポロジ フィルターの暗証番号 (pin) を出力するアナログ信号に PCM のデータを変換します。 FM シンセサイザーまたはトポロジのフィルターの KSPIN に物理的に接続されているウェーブ シンセサイザー フィルター\_TOPO\_SYNTHOUT\_SRC 暗証番号 (pin) が MIDI のデータをトポロジ フィルターの暗証番号 (pin) を出力するアナログ信号に同様に変換します。 トポロジのフィルターは、これら 2 つの pin をアナログ信号が混在し、スピーカーを混在信号を出力します。

同じアダプター カードの場合は、他のハードウェア デバイスを表すその他のフィルターにトポロジ フィルターの物理的な接続は、他の種類の接続のフィルターと区別する必要があります。 たとえば、特定のピン wave、MIDI、および DirectMusic でフィルターでく接続または切断ソフトウェア管理下にあります。

アダプターのドライバー、デバイスの起動中に呼び出すことによって、トポロジのフィルターの物理的な接続を登録します[ **PcRegisterPhysicalConnection** ](https://msdn.microsoft.com/library/windows/hardware/ff537726)接続ごとに 1 回です。 ポート ドライバーに応答するためにこの情報が必要[ **KSPROPERTY\_PIN\_PHYSICALCONNECTION** ](https://msdn.microsoft.com/library/windows/hardware/ff565205)プロパティの get 要求。

 

 




