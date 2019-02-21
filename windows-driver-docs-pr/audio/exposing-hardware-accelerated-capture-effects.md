---
title: ハードウェア アクセラレータによるキャプチャの効果を公開します。
description: ハードウェア アクセラレータによるキャプチャの効果を公開します。
ms.assetid: 032139e8-e758-4d63-b8c1-ca61c958b20b
keywords:
- ノイズの抑制 WDK オーディオ
- NS WDK オーディオ
- ハードウェア アクセラレータ WDK DirectSound、キャプチャの効果
- ハードウェア アクセラレータを使用したキャプチャ効果 WDK オーディオ
- アコースティック エコー キャンセル WDK オーディオ
- AEC WDK オーディオ
- ノードのチェーンの WDK オーディオ
- WDK DirectSound ノード順序要件
- 論理ピン WDK オーディオ
- ノードの暗証番号 (pin) の割り当ての WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8f0167052142b57fe0c940e3160c0ea5da92272
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536062"
---
# <a name="exposing-hardware-accelerated-capture-effects"></a>ハードウェア アクセラレータによるキャプチャの効果を公開します。


## <span id="exposing_hardware_accelerated_capture_effects"></span><span id="EXPOSING_HARDWARE_ACCELERATED_CAPTURE_EFFECTS"></span>


Windows XP 以降では、WDM オーディオ フレームワークは DirectSound を通じて公開されているオーディオ キャプチャの効果のハードウェア アクセラレーションをサポートします。 これらの効果には、アコースティック エコー キャンセル (AEC) とノイズの抑制 (NS) が含まれます。 DirectSoundCapture アプリケーション ハードウェア アクセラレータによる AEC および NS の使用を有効にする方法については、Microsoft Windows SDK のドキュメントを参照してください。

ミニポート ドライバーでは、基になるデバイスの機能によって、これらの効果の一部のハードウェア アクセラレータを公開できます。 AEC および NS 効果のハードウェアの機能を公開するには、AEC で各ピンのフィルター ドライバーの実装はこれらの要件を満たす必要があります。

-   Pin をグラフに組み込めるハードウェア効果を表すノード チェーン内の個別のノードを含める必要があります。 AEC と NS 効果 KS ノード型は次の Guid を指定します。[**KSNODETYPE\_音響\_エコー\_キャンセル**](https://msdn.microsoft.com/library/windows/hardware/ff537150)
    [**KSNODETYPE\_ノイズ\_を抑制します。**](https://msdn.microsoft.com/library/windows/hardware/ff537182)
-   ピン AEC および NS ノードをサポートする必要があります、 [KSPROPSETID\_全般](https://msdn.microsoft.com/library/windows/hardware/ff566576)プロパティが設定され、クエリされるときに、製造元に関する情報を提供する必要があります、 [ **KSPROPERTY\_全般\_COMPONENTID** ](https://msdn.microsoft.com/library/windows/hardware/ff565171)プロパティ。

-   ピン AEC および NS ノードをサポートする必要があります、 [KSPROPSETID\_TopologyNode](https://msdn.microsoft.com/library/windows/hardware/ff537491)プロパティ セットとその 2 つのプロパティ。

    [**KSPROPERTY\_TOPOLOGYNODE\_を有効にする**](https://msdn.microsoft.com/library/windows/hardware/ff537431)効果を使用します。

    [**KSPROPERTY\_TOPOLOGYNODE\_リセット**](https://msdn.microsoft.com/library/windows/hardware/ff537434)効果を既定の状態にリセットします。

-   ピン AEC および NS ノードの次のプロパティをサポートする必要があります、 [KSPROPSETID\_オーディオ](https://msdn.microsoft.com/library/windows/hardware/ff537440)プロパティ セット。[**KSPROPERTY\_オーディオ\_CPU\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537255)
    [**KSPROPERTY\_オーディオ\_アルゴリズム\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff537240)
-   Pin は、KSPROPSETID の次のプロパティをサポートする必要があります\_オーディオ プロパティ セット。[**KSPROPERTY\_オーディオ\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff537297)
    [**KSPROPERTY\_オーディオ\_待機時間**](https://msdn.microsoft.com/library/windows/hardware/ff537286)
-   Pin がそのデータ範囲の機能を公開する必要があります (を参照してください[暗証番号 (pin) のデータ範囲は、プロパティの積集合](pin-data-range-and-intersection-properties.md))。

ハードウェア アクセラレータによる AEC および NS ノードを公開するための特定の要件は次に示します。

### <a name="span-idacousticechocancellationspanspan-idacousticechocancellationspanspan-idacousticechocancellationspanacoustic-echo-cancellation"></a><span id="Acoustic_Echo_Cancellation"></span><span id="acoustic_echo_cancellation"></span><span id="ACOUSTIC_ECHO_CANCELLATION"></span>アコースティック エコー キャンセル

PCM のミニポート ドライバーでは、両方でキャプチャするためのトポロジの形式で AEC のハードウェア サポートを公開し、この追加の要件を満たしているストリームを表示します。

-   Pin は、AEC のノードを含める必要があります ([**KSNODETYPE\_音響\_エコー\_キャンセル**](https://msdn.microsoft.com/library/windows/hardware/ff537150))、順序付けられたノードのチェーン (参照内の適切な位置で指定する必要があります下記参照)。

### <a name="span-idnoisesuppressionspanspan-idnoisesuppressionspanspan-idnoisesuppressionspannoise-suppression"></a><span id="Noise_Suppression"></span><span id="noise_suppression"></span><span id="NOISE_SUPPRESSION"></span>ノイズの抑制

PCM のミニポート ドライバーには、この追加の要件を満たしているキャプチャ ストリームするためのトポロジの形式で NS 用ハードウェア サポートが公開しています。

-   Pin は、NS ノードを含める必要があります ([**KSNODETYPE\_ノイズ\_抑制**](https://msdn.microsoft.com/library/windows/hardware/ff537182))、順序付けられたノードのチェーン (下記参照) 内の適切な位置で指定する必要があります。

### <a name="span-idnode-chainorderingspanspan-idnode-chainorderingspanspan-idnode-chainorderingspannode-chain-ordering"></a><span id="Node-Chain_Ordering"></span><span id="node-chain_ordering"></span><span id="NODE-CHAIN_ORDERING"></span>ノード チェーンの順序付け

現時点では、DirectSound キャプチャ効果のアーキテクチャでは、ノードは、アプリケーションによって要求された順番で指定する必要があります。 その結果、ミニポート ドライバーがそのノードを指定します順序はによって使用される順序、一致する必要があります、 [AEC システム フィルター](aec-system-filter.md) (Aec.sys) のソフトウェアの AEC、およびアルゴリズムを実装します。

ハードウェア アクセラレータを有効にするには、ドライバーは、次の順序でハードウェアによって実装される効果を指定する必要があります。

[**KSNODETYPE\_ADC**](https://msdn.microsoft.com/library/windows/hardware/ff537153)

[**KSNODETYPE\_音響\_エコー\_キャンセル**](https://msdn.microsoft.com/library/windows/hardware/ff537150)

[**KSNODETYPE\_ノイズ\_を抑制します。**](https://msdn.microsoft.com/library/windows/hardware/ff537182)

相対的な順序が維持される限り、この一覧に実装されていないすべての効果を省略できますに注意してください。

### <a name="span-idaecnodepinassignmentsspanspan-idaecnodepinassignmentsspanspan-idaecnodepinassignmentsspanaec-node-pin-assignments"></a><span id="AEC_Node_Pin_Assignments"></span><span id="aec_node_pin_assignments"></span><span id="AEC_NODE_PIN_ASSIGNMENTS"></span>AEC ノード暗証番号 (pin) の割り当て

アダプターのドライバーの配列を使用して[ **PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)フィルター内の接続を指定する構造体。 配列の各要素には、1 つの接続は、ノード間、pin をノード、または暗証番号 (pin)-pin がについて説明します。 詳細については、次を参照してください。[ノードと接続](nodes-and-connections.md)します。

PCCONNECTION を使用する\_記述子構造体ドライバー ライターで、ノードに「論理」ピンが割り当てられます。 これらはノード自体が「ピン」であり、フィルター内の接続を指定するためだけに使用されます。 これは、他のフィルターへの接続に使用される外部 pin では、フィルターとは対照的です。

次の表は、暗証番号 (pin) Id を表示し、アダプター ドライバーが 4 つの論理ピン AEC ノードに割り当てる必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">暗証番号 (pin) の ID パラメーターの名前</th>
<th align="left">Value</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_RENDER_IN</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>レンダリングのストリームのシンクのピン (ノードの入力)</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_RENDER_OUT</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ソース pin (出力のノード) のストリームを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_IN</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>シンクのキャプチャのストリームの pin (ノードの入力)</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODEPIN_AEC_CAPTURE_OUT</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>キャプチャのストリームのソース pin (ノードの出力)</p></td>
</tr>
</tbody>
</table>

 

上記の表に、暗証番号 (pin) Id は、Ksmedia.h ヘッダー ファイルで定義されます。

次のコード例では、アダプターのドライバーが、AEC のノードと、NS ノードの両方を含む AEC フィルターの内部のトポロジを指定する方法を示します。

```cpp
    // AEC Filter Topology

    // Pin IDs for external pins on AEC filter
    #define ID_CaptureOutPin   0   // microphone stream
    #define ID_CaptureInPin    1
    #define ID_RenderOutPin    2   // speaker stream
    #define ID_RenderInPin     3

    // Generic pin IDs for simple node with one input and one output
    #define NODE_INPUT_PIN     1
    #define NODE_OUTPUT_PIN    0

    // Node IDs
    #define NODE_ID_AEC        0   // acoustic echo cancellation
    #define NODE_ID_NS         1   // noise suppression

    // The array below defines the internal topology of an
    // AEC filter that contains an AEC node and an NS node.

    const PCCONNECTION_DESCRIPTOR AecConnections[] = {
        { PCFILTER_NODE, ID_RenderInPin,       NODE_ID_AEC,    KSNODEPIN_AEC_RENDER_IN  },
        { NODE_ID_AEC,   KSNODEPIN_AEC_RENDER_OUT,   PCFILTER_NODE,  ID_RenderOutPin    },
        { PCFILTER_NODE, ID_CaptureInPin,      NODE_ID_AEC,    KSNODEPIN_AEC_CAPTURE_IN },
        { NODE_ID_AEC,   KSNODEPIN_AEC_CAPTURE_OUT,  NODE_ID_NS,     NODE_INPUT_PIN     },
        { NODE_ID_NS,    NODE_OUTPUT_PIN,      PCFILTER_NODE,  ID_CaptureOutPin   }
    };
```

上記のコード例で AecConnections 配列では、次の図に表示されるフィルターのトポロジを定義します。

![aec フィルターの内部のトポロジを示す図](images/aectopo.png)

上記の図は、データ フローの方向を示す破線の矢印の付いたフィルター内の各接続を表します。 図 5 つの接続の合計が表示されます。 各接続は、コード例では、AecConnections 配列内の 5 つの要素のいずれかに対応します。

 

 




