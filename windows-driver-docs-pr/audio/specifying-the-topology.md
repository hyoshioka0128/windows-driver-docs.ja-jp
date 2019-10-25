---
title: トポロジの指定
description: トポロジの指定
ms.assetid: 265cbd87-d40f-4ead-ba6e-a1cef51baf95
keywords:
- WDM オーディオドライバー WDK、トポロジ
- オーディオドライバー WDK、トポロジ
- トポロジ WDK オーディオ
- KS トポロジ WDK オーディオ
- カーネルストリーミングトポロジ WDK オーディオ
- PortCls WDK audio, トポロジ
- ポートドライバー WDK オーディオ、トポロジ
- トポロジポートドライバー WDK オーディオ
- オーディオミックストポロジ WDK オーディオ
- KS WDK オーディオ、トポロジをピン留めする
- KS WDK audio, トポロジをフィルター処理します
- WDK audio, KS をフィルター処理します。
- WDK audio, KS をピン留めする
- オーディオアダプター WDK、トポロジ
- ブリッジピン WDK オーディオ
- KS プロパティ WDK audio
- プロパティが WDK オーディオを要求する
- PCM 波出力 WDK オーディオ
- S/PDIF パススルー WDK オーディオ
- オーディオ WDK の混合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f165011fdf6cfc7ee4ebe3b1da5c250c3d5b3db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832426"
---
# <a name="specifying-the-topology"></a>トポロジの指定


ハードウェアベンダーが、wave デバイスと MIDI デバイス用に書き込むミニポートドライバーを決定したら、次の手順は、これらのデバイスのカーネルストリーミング (KS) トポロジを表すことです。 KS トポロジは、オーディオストリームまたは MIDI ストリームが各デバイスを流れるときに従うデータパスを記述する一連のデータ構造で構成されています。 このトポロジを通じて、ドライバーは各パスに存在する制御ノード (ボリュームコントロールなど) を公開します。 通常、アプリケーションでは、Windows マルチメディアミキサー*Xxx*関数を使用して、各パスに沿ってノードのシーケンスを列挙することによってトポロジを探索します。 たとえば、ボリュームレベルの制御ノードを検出した後、アプリケーションはそのノードにボリュームレベルを設定できます。 Windows マルチメディアの詳細については、Microsoft Windows SDK のドキュメントを参照してください。 ミキサ*Xxx*関数による KS トポロジの表現の詳細については、「 [Kernel Streaming Topology TO Audio mixer API Translation](kernel-streaming-topology-to-audio-mixer-api-translation.md)」を参照してください。

PortCls では、WavePci、WaveCyclic、WaveRT、MIDI、DMus、トポロジの6つのポートドライバーが提供されています。 (WaveRT は Windows Vista 以降で使用可能であり、推奨される方法です)。トポロジポートドライバーは、wave および MIDI デバイスからのレンダリングストリームをミキシングするオーディオアダプターの回路の一部を制御します。 また、入力ジャックからのキャプチャストリームの選択も制御します。 少し紛らわしい名前でも、トポロジポートドライバーは、オーディオアダプターのすべてのトポロジを具体化するわけではありませんが、通常はその一部が含まれています。 他のポートドライバーは、アダプターのトポロジの残りの部分を提供します。

次の表に示すように、各ポートドライバーは対応するミニポートドライバーとペアになり、オーディオアダプターの特定のデバイス (wave、MIDI、またはミキサー) を表す[KS フィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-filters)を形成します。

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
<td align="left"><p>Wave 出力ストリームをアナログオーディオ信号に変換するか、アナログオーディオ信号を wave 入力ストリームに変換する wave デバイスを表します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MIDI または DMus フィルター</p></td>
<td align="left"><p>MIDI ストリームを再生またはキャプチャする MIDI デバイスを表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>トポロジフィルター</p></td>
<td align="left"><p>アダプターのミキサー回路を表します。</p></td>
</tr>
</tbody>
</table>

 

ミニポートドライバーは、デバイスに含まれるアダプタートポロジの部分の定義など、フィルターのデバイス固有の機能を実装します。 ポートドライバーは、フィルターの種類ごとに、オペレーティングシステムとの通信を含む汎用フィルター操作を処理します。

各フィルターには、フィルターに入力して残すオーディオデータのストリームの経路として機能する1つ以上の[KS ピン](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-pins)があります。 通常、トポロジフィルターのピンは、アダプターの回路にある接続された接続を使用して、wave、MIDI、および DMus フィルターのピンに関連付けられています。 これらのフィルターとその相互接続は、アダプターのトポロジを具体化する KS フィルターグラフを形成します。

次の図は、サンプルオーディオアダプターのトポロジを示しています。

![オーディオアダプターのトポロジを示す図](images/topoexample.png)

上の図では、最上位レベルのトポロジは、MIDI、Wave*Xxx*、およびトポロジフィルター間の接続で構成されています。 さらに、各フィルターには独自の内部トポロジがあります。これは、フィルターと各パスに配置されているコントロールノードから成るデータパスで構成されます。 ノードには、次の表に示すようなラベルが付けられます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Label</th>
<th align="left">説明</th>
<th align="left">KS ノード型 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>シン</p></td>
<td align="left"><p>シンセサイザーノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer" data-raw-source="[&lt;strong&gt;KSNODETYPE_SYNTHESIZER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)"><strong>KSNODETYPE_SYNTHESIZER</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>DAC</p></td>
<td align="left"><p>デジタル-オーディオコンバーターノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac" data-raw-source="[&lt;strong&gt;KSNODETYPE_DAC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)"><strong>KSNODETYPE_DAC</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>ADC</p></td>
<td align="left"><p>アナログ-デジタルコンバーターノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc" data-raw-source="[&lt;strong&gt;KSNODETYPE_ADC&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc)"><strong>KSNODETYPE_ADC</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>[ボリューム]</p></td>
<td align="left"><p>ボリュームレベルの制御ノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume" data-raw-source="[&lt;strong&gt;KSNODETYPE_VOLUME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)"><strong>KSNODETYPE_VOLUME</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>Mute</p></td>
<td align="left"><p>ミュートコントロールノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUTE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mute)"><strong>KSNODETYPE_MUTE</strong></a></td>
</tr>
<tr class="even">
<td align="left"><p>合計</p></td>
<td align="left"><p>合計ノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum" data-raw-source="[&lt;strong&gt;KSNODETYPE_SUM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)"><strong>KSNODETYPE_SUM</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p>マルチプレクサー</p></td>
<td align="left"><p>マルチプレクサーノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux" data-raw-source="[&lt;strong&gt;KSNODETYPE_MUX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-mux)"><strong>KSNODETYPE_MUX</strong></a></td>
</tr>
</tbody>
</table>

 

上の図では、オーディオアダプターの左側のピンが、データストリームがシステムバスからアダプターに入力する論理接続 (物理的な接続ではない) を表しています。または、アダプターからシステムバスを入力します。 これらの pin は、アダプターの外部にある他のフィルター (表示されません) のソースおよびシンクのピンに論理的に接続されます。 通常、これらのフィルターは、アダプタートポロジと共に、ミキサー*Xxx*関数を使用してアプリケーションでトポロジを調べることができる、より大きなフィルターグラフを形成するソフトウェアモジュールです。 たとえば、前の図の "PCM Wave Out" というラベルが付いた pin は、Windows のユーザーモードオーディオエンジンに論理的に接続されています。 これらの論理接続は、システムバスを介した DMA 転送によって維持されます。

これに対して、トポロジフィルターの左端のピンは、MIDI フィルターと Wave*Xxx*フィルターのピンに物理的に接続されています。 これらの接続は固定可能で、ソフトウェアで変更することはできません。

オーディオアダプターの右側にあるブリッジピンは、システムシャーシのオーディオジャックを表します。 これらのピンは、KS フィルターグラフと外部世界の境界をブリッジするため、*ブリッジピン*と呼ばれます。

フィルター、ピン、およびノードには、通常、オーディオドライバーのクライアント (カーネルモードコンポーネントまたはユーザーモードアプリケーション) がアクセスできるプロパティがあります。 クライアントは、プロパティの現在の値を照会したり、プロパティ値を変更したりするために、フィルター、ピン、またはノードに[KS プロパティ要求](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties)を送信できます。 たとえば、ボリュームレベルの制御ノードには、 [ **\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)プロパティがあります。このプロパティは、クライアントが KS プロパティ要求を通じて変更できます。 合計ノードは、通常はプロパティを持たないノード型の一例です。

わかりやすくするために、前の図の Wave*Xxx*フィルターでは、システムバスから PCM 波出力ストリームを受け付けるための pin が1つだけ提供されています。 これに対して、一部の wave デバイスでは、PCM wave 出力用に複数のピンが提供されており、ピンに入るストリームを内部でミキシングするためのハードウェアが含まれています。 これらのデバイスは、アプリケーションのサウンドバッファーから再生される PCM ストリームを受け入れることによって、DirectSound を使用するアプリケーションのハードウェアの高速化を実現します。 DirectSound でこれらのピンを使用するには、「 [WDM オーディオの Directsound ハードウェア高速化](directsound-hardware-acceleration-in-wdm-audio.md)」で説明されているように、2次元 (2-d) および3次元 (3 d) 処理用に追加のノードを提供する必要があります。

この種のハードウェアアクセラレータは、Windows Server 2003、Windows XP、Windows 2000、および Windows Me/98 でサポートされていますが、Windows Vista ではサポートされていません。 Windows Vista では、古い wave デバイスでハードウェアアクセラレータの pin が使用されません。

上の図では、MIDI、Wave*Xxx*、およびトポロジ間の物理接続は、すべてのトランスポートアナログオーディオ信号をフィルター処理します。 ただし、異なるトポロジデバイスでは、MIDI および wave デバイスからデジタル出力ストリームを受け取り、デジタルミックスをデジタル化して、デジタルミックスをアナログ出力信号に変換することで、同様の効果を得ることができます。

上の図の左下隅にある "非 PCM Wave Out" ピンは、S/PDIF パススルー形式の PCM 以外の出力ストリームを受け付けます (AC-3-over S/PDIF または WMA Pro-over-S/PDIF など)。 デバイスは、これらの形式のいずれかを使用して、データをデコードせずに、単純に S/PDIF リンクを介して圧縮データを転送します。 このため、前の図の右下隅にある "S/PDIF Out" ピンへのデータパスには、ボリュームまたはミュートノードが含まれていません。 PCM 以外のオーディオ形式と S/PDIF パススルー伝送の詳細については、「 [Pcm 以外の Wave 形式のサポート](supporting-non-pcm-wave-formats.md)」を参照してください。 その他の情報については、オーディオ[テクノロジ](https://go.microsoft.com/fwlink/p/?linkid=8751)の web サイトの「 *audio DRIVER Support for WMA Pro OVER S/PDIF 形式*」というホワイトペーパーを参照してください。

ミニポートドライバーは、 [**Pcfilter\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)構造の形式でポートドライバーにトポロジを提示します。 この構造体は、すべてのフィルターのピンとノードを記述し、ピンとノードが相互に接続する方法を指定します。

前の図に示すように、モノリシックトポロジフィルターを設計するのではなく、オーディオアダプターのミキサー回路を複数のトポロジフィルターに分割できます。 たとえば、前の図では、スピーカーを駆動するデータパスが1つのトポロジフィルターとして実装されており、入力デバイスからオーディオデータをキャプチャするデータパスを別のトポロジフィルターとして実装できます。 特定のトポロジフィルターのデータパスが使用されていない場合、アダプター全体を無効にすることなく、アダプターのその部分の電源を切ることができます。 詳細については、「[動的オーディオサブデバイス](dynamic-audio-subdevices.md)」を参照してください。

 

 




