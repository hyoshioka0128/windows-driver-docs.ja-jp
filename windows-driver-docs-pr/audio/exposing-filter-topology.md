---
title: フィルター トポロジの公開
description: フィルター トポロジの公開
ms.assetid: bf791f40-b2fb-48fe-8350-3b926db4ead7
keywords:
- トポロジフィルター WDK オーディオ
- フィルタートポロジ WDK オーディオ
- KS WDK audio, トポロジをフィルター処理します
- フィルタートポロジの公開
- オーディオフィルター WDK オーディオ、トポロジの公開
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8420601c0c8329f6026920736bfa3e8e738165b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833413"
---
# <a name="exposing-filter-topology"></a>フィルター トポロジの公開


## <span id="exposing_filter_topology"></span><span id="EXPOSING_FILTER_TOPOLOGY"></span>


ミニポートドライバーは、ピン、ノード、および接続の観点から、KS フィルターの内部トポロジについて説明します。 このトポロジでは、フィルターを使用してデータフローパスを指定し、プロパティ要求の論理ターゲット (ピンとノード) も定義します。 フィルター内トポロジは、フィルターの基になっているハードウェアデバイスの内部構造を論理的に表現したものです。 ミニポートドライバーは、ピン、ノード、および接続記述子の静的配列を使用して、このトポロジについて説明します。

-   ピンは[**Pcpin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)の構造体の静的配列で指定されます。 各 pin には、配列内で序数となっている ID があります。

-   ノードは、 [**pcnode\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcnode_descriptor)構造体の静的配列で指定されます。 各ノードには、配列内で序数となっている ID があります。

-   接続 (ピン留めピン、ピン留めノード、またはノードからノードへのピン留め) は、 [**Pcconnection\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))構造体の静的配列に指定されています。

ミニポートドライバーは、 [**IMiniport:: GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)メソッドから出力する[**pcfilter\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)構造体に、この3つの配列を公開します。

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>よう

次のコード例では、1つの入力ピンと1つの出力ピンを持つ単純な KS フィルターの内部トポロジを指定します。 このフィルターには、ボリュームレベルのコントロールである1つのノードが含まれています。

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

次の図は、上記のサンプルコードで説明されているフィルターのトポロジを示しています。

![単純なフィルタートポロジを示す図](images/audtop.png)

このフィルターは、 [IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)オブジェクトを PortCls システムドライバーによって作成された[iporttopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)オブジェクトにバインドすることによってアダプタードライバーが形成する[トポロジフィルター](topology-filters.md)の簡単な例です。 フィルターの入力 (シンク) と出力 (ソース) の各ピンの名前は、KSPIN\_WAVEOUT\_SRC と KSPIN\_スピーカー\_DST です。 両方のピンがアナログ信号を搬送します。 **ミキサー** API は、ソースとターゲットのミキサ線としてこれらのピンへの接続を公開します (MIXERLINE\_componenttype\_SRC\_WAVEOUT および MIXERLINE\_COMPONENTTYPE\_DST\_講演)。

次の表は、KS ピンとミキサーの線のマッピングについて説明する際に、混乱の原因となる可能性があることを示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ピンの名前</th>
<th align="left">ミキサー API の用語</th>
<th align="left">KS フィルターの用語</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSPIN_WAVEOUT_SRC</p></td>
<td align="left"><p>ソースミキサーの線</p></td>
<td align="left"><p>シンク pin</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSPIN_SPEAKERS_DST</p></td>
<td align="left"><p>ターゲットミキサーの線</p></td>
<td align="left"><p>ソースピン</p></td>
</tr>
</tbody>
</table>

 

KSPIN\_WAVEOUT\_SRC はソースミキサーラインであり、KSPIN\_スピーカー\_DST はソース pin です。 詳細については、「[カーネルストリーミングトポロジからオーディオミキサー API への変換](kernel-streaming-topology-to-audio-mixer-api-translation.md)」の KS およびミキサーラインの用語に関する説明を参照してください。

また、"KSPIN\_WAVEOUT\_SRC" という名前には "WAVEOUT" が含まれています。これは、ピンが wave 形式のデジタルデータを保持しているのに対し、WaveCyclic または WavePci 型のフィルターである wave フィルターによって生成されるアナログ信号を伝達するためです。 Wave フィルターは、wave ストリームをアナログ信号に変換するオーディオアダプターのハードウェアの部分を表します。 KSPIN\_スピーカーをピン留めすると、スピーカーのセットを駆動するアナログ信号が出力さ\_ます。

このフィルターには、1つのノードである KSK ノード\_WAVEOUT\_ボリュームが含まれています。これは、**ミキサー** API がボリュームコントロール (MIXERCONTROL\_CONTROLTYPE\_ボリューム) として表現します。 ボリュームコントロールの KS ノードタイプは[**KSNODETYPE\_volume**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)です。 この種類のすべてのノードでは、 [**Ksk プロパティ\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)プロパティがサポートされています。このプロパティは、フィルターのクライアントがボリュームレベルを制御するために使用します。

ボリュームノードには、0と1の番号が付いた2つの "論理" ピンがあります。 MiniportConnections 配列によって指定された2つの接続は、データフローの方向を示す破線の矢印によって図で表されます。 各接続は、配列内の2つの要素のいずれかによって記述されます。

KSPIN\_WAVEOUT\_SRC と KSPIN\_\_スピーカーは両方とも*ブリッジピン*です。つまり、アダプター内の接続された接続を表します。 前のサンプルコードでは、MiniportPins 配列内の2つのピン記述子は両方とも、IRP フロー方向を KSPIN\_通信\_NONE として指定しています。ブリッジピンは送信も受信の両方の Irp でもありません。 2つのピン記述子は、次のように定義されている PinDataRangePointersBridge 配列も参照します。

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

PinDataRangePointersBridge 配列は、アナログオーディオ信号を伝送するブリッジピンのデータ範囲を定義します。 詳細については、「[オーディオフィルターグラフ](audio-filter-graphs.md)のブリッジピンの説明」を参照してください。

より複雑なトポロジの例については、「[トポロジフィルター](topology-filters.md)」を参照してください。

 

 




