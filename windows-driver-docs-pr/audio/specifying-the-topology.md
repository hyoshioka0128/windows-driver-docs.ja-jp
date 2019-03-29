---
title: トポロジの指定
description: トポロジの指定
ms.assetid: 265cbd87-d40f-4ead-ba6e-a1cef51baf95
keywords:
- WDM オーディオ ドライバー WDK、トポロジ
- オーディオ ドライバー WDK、トポロジ
- トポロジの WDK オーディオ
- KS トポロジ WDK オーディオ
- ストリーミング トポロジ WDK のオーディオのカーネル
- PortCls WDK オーディオ、トポロジ
- ポート ドライバー WDK のオーディオ、トポロジ
- トポロジ ポート ドライバー WDK オーディオ
- オーディオの混合トポロジ WDK オーディオ
- KS は、WDK オーディオ、トポロジをピン留め
- KS は、WDK オーディオ、トポロジをフィルター処理します。
- WDK のオーディオ、KS をフィルター処理します。
- ピンの WDK オーディオ、KS
- オーディオ アダプター WDK、トポロジ
- ブリッジ ピン WDK オーディオ
- KS プロパティ WDK オーディオ
- プロパティ要求 WDK オーディオ
- PCM wave 出力 WDK オーディオ
- S/PDIF パススルー WDK オーディオ
- オーディオの WDK の混在
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0645a9a1bebbcb6c520ea8e0fe69d1287eccd75
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350399"
---
# <a name="specifying-the-topology"></a>トポロジの指定


ハードウェア ベンダーでは、ミニポート ドライバー wave および MIDI デバイスの書き込みを決定したら後、次の手順では、これらのデバイス (KS) トポロジをストリーミングするカーネルを表します。 KS トポロジは、オーディオまたは MIDI ストリームに従って各デバイスを通じたデータのパスを記述するデータ構造のセットで構成されます。 このトポロジでは、ドライバーは、各パス上にあるコントロールのノード (たとえば、ボリューム コントロール) を公開します。 通常、アプリケーションが Windows のマルチ メディア ミキサーを使用*Xxx*各パスに沿ってノードのシーケンスを列挙することによって、トポロジを探索する関数。 たとえば、ボリューム レベルの制御ノードを検出したら、アプリケーション レベルを設定できます、ボリュームそのノード上。 Windows のマルチ メディアの詳細については、Microsoft Windows SDK のドキュメントを参照してください。 ミキサーで KS トポロジの表現の詳細については*Xxx*関数を参照してください[オーディオ Mixer API 翻訳にカーネル ストリーミング トポロジ](kernel-streaming-topology-to-audio-mixer-api-translation.md)します。

PortCls には、6 つのポートのドライバーが用意されています。WavePci、WaveCyclic、WaveRT、MIDI、Dmu およびトポロジ。 (WaveRT は Windows Vista から利用できましたがおよび推奨されるアプローチです)。トポロジのポート ドライバーでは、まとめて wave および MIDI デバイスからレンダリング ストリームが混在するオーディオ アダプター回路の部分を制御します。 入力ジャックからキャプチャ ストリームの選択も制御します。 少し誤解されやすい名称にもかかわらずトポロジ ポート ドライバーはオーディオのアダプターのトポロジのすべてを具体化できません、その大部分にが含まれては通常します。 その他のポート ドライバーでは、アダプターのトポロジの残りの部分を投稿します。

各ポート ドライバーはフォームに対応するミニポート ドライバーと組み合わせて、 [KS フィルター](https://msdn.microsoft.com/library/windows/hardware/ff567644)オーディオのアダプターの特定のデバイス (wave、MIDI、またはミキサー) を表す次の表に示すようにします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィルターの種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Wave<em>Xxx</em>フィルター</p></td>
<td align="left"><p>Wave デバイス アナログ オーディオ信号に wave 出力ストリームを変換またはアナログ オーディオ信号を wave 入力ストリームに変換を表します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MIDI または Dmu のフィルター</p></td>
<td align="left"><p>再生または MIDI ストリームをキャプチャする MIDI デバイスを表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>トポロジのフィルター</p></td>
<td align="left"><p>アダプターのミキサー回路を表します。</p></td>
</tr>
</tbody>
</table>

 

ミニポート ドライバーでは、デバイスを含むアダプター トポロジの一部の定義など、フィルターのデバイス固有の関数を実装します。 ポートのドライバーは、フィルターの種類ごとに、オペレーティング システムとの通信をなど、汎用フィルター操作で処理されます。

各フィルターには、1 つまたは複数[KS ピン](https://msdn.microsoft.com/library/windows/hardware/ff567669)を入力し、フィルターのままにするオーディオ データのストリームの経路として機能します。 通常、wave、MIDI、トポロジのフィルターのピンがピンに関連付けられているし、アダプター回路で有線接続経由の Dmu をフィルター処理します。 これらのフィルターとの相互接続をまとめて、アダプターのトポロジを具体化する KS フィルター グラフを形成します。

次の図は、例のオーディオ アダプターのトポロジを示します。

![オーディオのアダプターのトポロジを示す図](images/topoexample.png)

MIDI、Wave 間の接続の前の図では、最上位レベルでトポロジがで構成されています。*Xxx*、およびトポロジ フィルター。 また、各フィルターでは、フィルターと制御ノード上の各パスを介したデータ パスから成る独自内部のトポロジ。 ノードは、次の表に示すようにラベル付けされます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">group1</th>
<th align="left">説明</th>
<th align="left">KS ノード タイプの GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>シンセサイザー</p></td>
<td align="left"><p>シンセサイザー ノード</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537203" data-raw-source="[&lt;strong&gt;KSNODETYPE_SYNTHESIZER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537203)"><strong>KSNODETYPE_SYNTHESIZER</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>DAC (DAC)</p></td>
<td align="left"><p>デジタル-オーディオ コンバーター ノード</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537158" data-raw-source="[&lt;strong&gt;KSNODETYPE_DAC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537158)"><strong>KSNODETYPE_DAC</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>ADC</p></td>
<td align="left"><p>アナログ/デジタル コンバーター ノード</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537153" data-raw-source="[&lt;strong&gt;KSNODETYPE_ADC&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537153)"><strong>KSNODETYPE_ADC</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>[ボリューム]</p></td>
<td align="left"><p>ボリューム レベルの制御ノード</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537208" data-raw-source="[&lt;strong&gt;KSNODETYPE_VOLUME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537208)"><strong>KSNODETYPE_VOLUME</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>Mute</p></td>
<td align="left"><p>ミュート用のコントロールのノード</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537178" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUTE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537178)"><strong>KSNODETYPE_MUTE</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>Sum</p></td>
<td align="left"><p>ノードの合計</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537196" data-raw-source="[&lt;strong&gt;KSNODETYPE_SUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537196)"><strong>KSNODETYPE_SUM</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>MUX</p></td>
<td align="left"><p>マルチプレクサーのノード</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537180" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537180)"><strong>KSNODETYPE_MUX</strong></a></td>
</tr>
</tbody>
</table>

 

上記の図では、オーディオのアダプターの左側にあるピンは、論理接続 (物理接続) データ ストリームをシステム バスからアダプターを入力またはアダプターからのシステム バスの入力を表します。 これらのピンは、外部アダプターにある他のフィルター (非表示) のソースとシンクのピンを論理的に接続されます。 通常、これらのフィルターには、アダプター トポロジと共に、ミキサーを使用してアプリケーションで探索できますトポロジが大きいフィルター グラフを形成するソフトウェア モジュール*Xxx*関数。 たとえば、上記の図で"PCM Wave Out"というラベルが付いたピンでは、Windows でユーザー モードのオーディオ エンジンに接続されます論理的に。 これらの論理的な関係は、システム バス経由で DMA 転送によって管理されます。

トポロジのフィルターの左端のピンは、MIDI と Wave のピンに物理的に接続されてこれに対し、*Xxx*フィルター。 これらの接続は、配線で接続されて、ソフトウェアでは変更できません。

ブリッジのオーディオのアダプターの右側にあるピンは、システムのシャーシのオーディオ ジャックを表します。 これらのピンと呼びます*ピンをブリッジ*KS フィルター グラフと、外部世界との間の境界をブリッジするためです。

フィルター、pin、およびノードは、通常、オーディオ ドライバーのクライアント (カーネル モードのコンポーネントまたはユーザー モード アプリケーション) にアクセス可能であるプロパティを持ちます。 クライアントが送信を[KS プロパティ要求](https://msdn.microsoft.com/library/windows/hardware/ff567671)フィルター、pin、またはノード プロパティの現在の値に対してクエリを実行するか、プロパティ値を変更します。 たとえば、ボリューム レベルの制御ノードは、 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)プロパティで、クライアントは、KS プロパティ要求を通じて変更できます。 合計ノードのプロパティを通常持たないノード型の例に示します。

わかりやすいように、Wave*Xxx*上の図にフィルターでは、システム バスから PCM wave 出力ストリームを受け入れるためピンが 1 つが用意されています。 これに対し、wave デバイスによっては PCM wave 出力の複数の pin を指定し、内部的には、pin の入力ストリームを混在させる場合のハードウェアを含みます。 これらのデバイスでは、ハードウェア アクセラレーション、アプリケーションのサウンド バッファーから再生する PCM ストリームをそのまま使用して、DirectSound を使用するアプリケーションを提供します。 」の説明に従って DirectSound でこれらのピンを使用するの他のノードの 2 次元 (2-d) と 3 次元 (3 D) を処理するを提供する必要があります[WDM オーディオでハードウェア アクセラレータを DirectSound](directsound-hardware-acceleration-in-wdm-audio.md)します。

Windows Server 2003、Windows XP、Windows 2000、および Windows でこの種類のハードウェア アクセラレータがサポートされている私が 98、Windows Vista ではサポートされません。 Windows Vista には、古い wave デバイスのハードウェアの高速化の pin の使用はしません。

上記の図では、MIDI、Wave 間の物理接続*Xxx*トポロジは、すべてのトランスポート アナログ オーディオ信号をフィルター処理とします。 ただし、トポロジのさまざまなデバイスでは、MIDI、wave デバイスからのデジタル出力ストリームを受け入れる、デジタルうまく組み合わせることで、デジタルの組み合わせをアナログ出力信号に変換する同様の効果を実現することがあります。

上記の図の左下隅にある"非 PCM Wave Out"ピン留めは、AC-3-フェールオーバー-S/PDIF または WMA Pro-オーバー-S/PDIF など、S/PDIF パススルー形式で PCM 非出力ストリームを受け入れます。 これらの形式のいずれかを使用して、デバイスだけです、圧縮されたデータ転送 S/PDIF リンク経由でデータをデコードすることがなくします。 このため、上の図の右下隅にある"S/PDIF Out"ピン アイコンへのデータ パスには、ボリュームまたはミュートのノードにありません。 オーディオ形式の非 PCM と S/PDIF パススルー送信の詳細については、次を参照してください。[非 PCM Wave 形式のサポート](supporting-non-pcm-wave-formats.md)します。 追加情報は、ホワイト ペーパーで使用できる*WMA Pro オーバー-S/PDIF 形式のオーディオ ドライバー サポート*で、[オーディオ テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8751)web サイト。

ミニポート ドライバーの形式でポート ドライバーには、そのトポロジを表示する、 [ **PCFILTER\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537694)構造体。 この構造体では、すべてのフィルターのピンと、ノードについて説明し、pin とノードが互いにどのように接続する方法を指定します。

モノリシック トポロジ フィルターを設計するのではなく 前の図に示すように、ミキサーの回路オーディオのアダプターでは、トポロジのいくつかのフィルターに分割できます。 たとえば、上記の図では、スピーカーを駆動するデータ パスは、1 つのトポロジのフィルターとして実装する可能性があり、入力デバイスからのオーディオ データをキャプチャするデータ パスは、別のトポロジのフィルターとして実装できます。 特定のトポロジ フィルター内のデータ パスが使用されていないときに、アダプターの部分の全体のアダプターを無効にしなくてもダウン電源できます。 詳細については、次を参照してください。[動的オーディオ サブデバイス](dynamic-audio-subdevices.md)します。

 

 




