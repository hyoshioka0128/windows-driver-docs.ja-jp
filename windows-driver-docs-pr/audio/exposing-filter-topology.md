---
title: フィルター トポロジの公開
description: フィルター トポロジの公開
ms.assetid: bf791f40-b2fb-48fe-8350-3b926db4ead7
keywords:
- トポロジのフィルターの WDK オーディオ
- トポロジの WDK オーディオをフィルター処理します。
- KS は、WDK オーディオ、トポロジをフィルター処理します。
- フィルターのトポロジを公開します。
- オーディオ フィルター WDK オーディオ、トポロジを公開します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbc0366e3fde41496139f495285a0b88ea6d87f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360056"
---
# <a name="exposing-filter-topology"></a>フィルター トポロジの公開


## <span id="exposing_filter_topology"></span><span id="EXPOSING_FILTER_TOPOLOGY"></span>


ミニポート ドライバーでは、pin、ノード、および接続の観点から KS フィルターの内部のトポロジについて説明します。 このトポロジでは、フィルターをデータ フロー パスを指定しもピンとノードのプロパティの要求の----論理のターゲットを定義します。 フィルター内のトポロジは、フィルターを基になるハードウェア デバイスの内部構造の論理表現です。 ミニポート ドライバーでは、暗証番号 (pin)、ノード、および接続記述子の静的な配列では、このトポロジについて説明します。

-   Pin がの静的配列で指定された[ **PCPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcpin_descriptor)構造体。 各ピンは、その序数を配列内の ID。

-   静的配列内のノードが指定されて[ **PCNODE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcnode_descriptor)構造体。 各ノードでは、その序数を配列には、ID があります。

-   接続 (暗証番号 (pin)-pin、暗証番号 (pin) とノードまたはノード間) の静的配列で指定[ **PCCONNECTION\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))構造体。

ミニポート ドライバーにこれら 3 つの配列を公開する、 [ **PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)構造からの出力をその[ **IMiniport::GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)メソッド。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、1 つの入力ピンと 1 つの出力ピンを持つ単純な KS フィルターの内部のトポロジを指定します。 フィルターには、ボリューム レベルの制御は、1 つのノードが含まれています。

```cpp
#define KSPIN_WAVEOUT_SRC  0
#define KSPIN_SPEAKERS_DST  1

PCPIN_DESCRIPTOR 
MiniportPins[] =
{
    {   // Pin 0 -- KSPIN_WAVEOUT_SRC
        0,0,0,  // InstanceCount
        NULL,   // AutomationTable
        {       // KsPinDescriptor
            0,                                          // InterfacesCount
            NULL,                                       // Interfaces
            0,                                          // MediumsCount
            NULL,                                       // Mediums
            SIZEOF_ARRAY(PinDataRangePointersBridge),   // DataRangesCount
            PinDataRangePointersBridge,                 // DataRanges
            KSPIN_DATAFLOW_IN,                          // DataFlow
            KSPIN_COMMUNICATION_NONE,                   // Communication
            &KSNODETYPE_LEGACY_AUDIO_CONNECTOR,         // Category
            NULL,                                       // Name
            0                                           // Reserved
        }
    },
    {   // Pin 1 -- KSPIN_SPEAKERS_DST
        0,0,0,  // InstanceCount
        NULL,   // AutomationTable
        {       // KsPinDescriptor
            0,                                          // InterfacesCount
            NULL,                                       // Interfaces
            0,                                          // MediumsCount
            NULL,                                       // Mediums
            SIZEOF_ARRAY(PinDataRangePointersBridge),   // DataRangesCount
            PinDataRangePointersBridge,                 // DataRanges
            KSPIN_DATAFLOW_OUT,                         // DataFlow
            KSPIN_COMMUNICATION_NONE,                   // Communication
            &KSNODETYPE_SPEAKER,                        // Category
            &KSAUDFNAME_VOLUME_CONTROL,                 // Name (This name shows up as the 
                                                        // playback panel name in SndVol32)
            0                                           // Reserved
        }
    }
};

#define KSNODE_WAVEOUT_VOLUME  0

PCNODE_DESCRIPTOR TopologyNodes[] =
{
    {   // KSNODE_WAVEOUT_VOLUME
        0,                      // Flags
        &AutomationVolume,      // AutomationTable
        &KSNODETYPE_VOLUME,     // Type
        &KSAUDFNAME_WAVE_VOLUME // Name
    }
};

PCCONNECTION_DESCRIPTOR MiniportConnections[] =
{ //FromNode---------------FromPin------------ToNode-----------------ToPin
  { PCFILTER_NODE,         KSPIN_WAVEOUT_SRC, KSNODE_WAVEOUT_VOLUME, 1 },
  { KSNODE_WAVEOUT_VOLUME, 0,                 PCFILTER_NODE,         KSPIN_SPEAKERS_DST }
};
```

次の図では、上記のサンプル コードで説明されているフィルターのトポロジを示します。

![単純なフィルターのトポロジを示す図](images/audtop.png)

このフィルターは、簡単な例を[トポロジ フィルター](topology-filters.md)、バインドすることによって、アダプターのドライバーを形成するその[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)オブジェクトを[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)オブジェクトをPortCls システム ドライバーを作成します。 フィルターには (シンク) の入力し、出力 (ソース) ピンの KSPIN 名前付け\_WAVEOUT\_src 属性と KSPIN\_スピーカー\_DST します。 両方のピンは、アナログ信号を実行します。 **ミキサー** API で公開元とコピー先のミキサー行としてこれらのピンへの接続 (MIXERLINE\_COMPONENTTYPE\_SRC\_WAVEOUT と MIXERLINE\_COMPONENTTYPE\_DST\_スピーカー)、それぞれします。

次の表は、KS ピン ミキサー行へのマッピングについて説明するときの混乱の潜在的な原因を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ピンの名前</th>
<th align="left">Mixer API の用語集</th>
<th align="left">KS フィルター用語集</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPIN_WAVEOUT_SRC</p></td>
<td align="left"><p>ミキサーのソース行</p></td>
<td align="left"><p>シンクのピン留めします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_SPEAKERS_DST</p></td>
<td align="left"><p>ミキサーの行を変換先</p></td>
<td align="left"><p>ソースの暗証番号 (pin)</p></td>
</tr>
</tbody>
</table>

 

注その KSPIN\_WAVEOUT\_SRC はソース ミキサー行、および KSPIN\_スピーカー\_DST がソースのピン留めします。 詳細については、KS とミキサー行の用語の説明を参照してください。[オーディオ Mixer API 翻訳にカーネル ストリーミング トポロジ](kernel-streaming-topology-to-audio-mixer-api-translation.md)します。

またを注意名前"KSPIN\_WAVEOUT\_SRC"wave フィルター、フィルターの種類 WaveCyclic によって生成されるアナログ信号を伝送だ、暗証番号 (pin) デジタル データのウェーブ フォーマットを実行するためではなく"WAVEOUT"が含まれていますかWavePci します。 Wave フィルターは、アナログ信号に wave ストリームを変換するオーディオのアダプターのハードウェアの部分を表します。 KSPIN をピン留め\_スピーカー\_DST は、一組のスピーカーを駆動するアナログ信号を出力します。

フィルターには、1 つのノード、KSNODE が含まれています。\_WAVEOUT\_、ボリュームを、**ミキサー** API は、ボリューム コントロールとして表します (MIXERCONTROL\_CONTROLTYPE\_ボリューム)。 ボリューム コントロールの KS ノード型は[ **KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)します。 これのすべてのノード タイプのサポート、 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)プロパティで、フィルターのクライアントを使用して、ボリューム レベルを制御します。

[ボリューム] ノードでは、番号は 0、1、2 つの「論理」の pin があります。 MiniportConnections 配列で指定されている 2 つの接続は、図のデータ フローの方向を指すの破線の矢印で表されます。 各接続は、配列内の 2 つの要素のいずれかで表されます。

KSPIN\_WAVEOUT\_src 属性と KSPIN\_スピーカー\_DST ピンは、どちらも*ピンをブリッジ*、有線接続、アダプターで表すことを意味します。 上記のサンプル コードでは両方 MiniportPins 配列内の 2 つの pin 記述子が KSPIN として IRP フロー方向を指定\_通信\_NONE の場合、ブリッジのピンは送信も Irp を受信するために適切な。 2 つの pin の記述子は、PinDataRangePointersBridge 配列は、次のように定義されているを参照してください。

```cpp
static KSDATARANGE PinDataRangesBridge[] =
{
   {
      sizeof(KSDATARANGE),
      0, 0, 0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_ANALOG),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE)
   }
};

static PKSDATARANGE PinDataRangePointersBridge[] =
{
    &PinDataRangesBridge[0]
};
```

PinDataRangePointersBridge 配列では、アナログのオーディオ信号を伝送するブリッジ pin のデータ範囲を定義します。 詳細については、ブリッジの pin での説明を参照してください。[オーディオ フィルター グラフ](audio-filter-graphs.md)します。

複雑なトポロジの例は、次を参照してください。[トポロジ フィルター](topology-filters.md)します。

 

 




