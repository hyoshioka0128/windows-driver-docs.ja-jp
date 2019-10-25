---
title: トポロジ ミニポート ドライバー
description: トポロジ ミニポート ドライバー
ms.assetid: 3e0b797e-2fa5-499b-a465-0f51f5433177
keywords:
- オーディオミニポートドライバー WDK、トポロジ
- ミニポートドライバー WDK オーディオ、トポロジ
- トポロジミニポートドライバー WDK オーディオ
- トポロジミニポートインターフェイス WDK オーディオ
- 接続記述子 WDK オーディオ
- ノードからの WDK オーディオ
- ノード内 WDK オーディオ
- 識別ノード識別子 WDK オーディオ
- オーディオ WDK の混合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5176f2976e8bbe98b13a840a30f01dce1131311
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832329"
---
# <a name="topology-miniport-driver"></a>トポロジ ミニポート ドライバー


## <span id="topology_miniport_driver"></span><span id="TOPOLOGY_MINIPORT_DRIVER"></span>


トポロジミニポートドライバーは、オーディオアダプターのミキサー回路におけるさまざまなハードウェア制御 (ボリューム、ミュートなど) を管理します。 このドライバーは、ミキサートポロジの*ノード*としてコントロールを列挙し、クライアントがノード間の相互接続を検出し、各ノードのコントロールパラメーターを照会および設定できるようにします。

[Sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)は、[オーディオフィルターグラフ](audio-filter-graphs.md)を構築するときに、アダプターのトポロジを確認します。 ミキサー API (Microsoft Windows SDK ドキュメントの「Windows マルチメディア」セクションで説明) は、トポロジノードをミキサーラインコントロールとして表し、SndVol32 などのユーザーモードアプリケーションに公開します。 詳細については、「 [SysTray と SndVol32](systray-and-sndvol32.md)」を参照してください。

トポロジミニポートドライバーは、ポートドライバーがミニポートドライバーを初期化するために使用するトポロジミニポートインターフェイスを実装する必要があります。 ミニポートインターフェイス[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)は、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)インターフェイスのメソッドを継承します。追加のメソッドはありません。 オーディオアダプタードライバーは、ポートオブジェクトの[Iporttopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)インターフェイスにミニポートオブジェクトの IMiniportTopology インターフェイスをバインドすることによって、[トポロジフィルター](topology-filters.md)を形成します。

通常、トポロジフィルターはアダプターのトポロジノードのほとんどを含みますが、アダプター内の他のデバイスには追加のトポロジノードが含まれる場合があります。 たとえば、wave フィルターとして表される wave デバイスには、DAC ([**KSNODETYPE\_dac**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)) ノードと Adc ([**KSNODETYPE\_adc**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc)) ノードが含まれる場合があります。

トポロジノードでのコントロールパラメーターのクエリと設定は、プロパティ要求によって実現されます。 各ノードタイプは、特定のプロパティまたはプロパティのセットに関連付けられています。 ノードは、1つのコントロール値のみをサポートする場合があります。 たとえば、ボリュームノード ([**KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)) には、現在のボリューム設定を示す値があります。 他のノードでは、複数のコントロール値がサポートする場合があります。 たとえば、3D ノード ([**KSNODETYPE\_3d\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)) では、いくつかの3d バッファーと3d リスナーのプロパティがサポートされています。 一方、sum ノード ([**KSNODETYPE\_sum**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum)) には制御値がありません。

トポロジミニポートドライバーでは、*接続記述子*([**pcconnection\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))) を使用して、2つのトポロジノード間の接続を記述します。 各接続が指示され、from ノードとからノードの両方が指定されます。 ノードには複数のピンがある場合があり、1つの pin によって実行される関数は、他のピンとは異なる場合があります。 あるピンを別の pin と区別するために、ミニポートドライバーはノードのピンに番号を付けます。 これらの pin 番号は、接続記述子に表示されます。 たとえば、状態変数フィルターには、3つの出力ピン (高、中間、低の各周波数の数字1、2、および 3) が含まれる場合があります。 ピン番号を付けると、ミニポートドライバーのクライアントは、どの接続がどのピンに関連付けられているかを判断できます。

接続記述子は、*識別ノード識別子*( [**PCFILTER\_ノード**](https://docs.microsoft.com/previous-versions/ff537695(v=vs.85))) を使用して、フィルターのピンとフィルター内のノードのピンを区別します。 オーディオアダプターのオーディオレンダリングおよびキャプチャデバイスに対するミキサー回路の接続された接続はそれぞれ、トポロジフィルターのピンとして表されます。 その他のトポロジフィルターピンは、アダプターカード上の lineout ジャックなど、外部の物理接続を表します。 トポロジフィルターのピンは、アダプターハードウェアの物理的で配線された接続を表します。 このため、ピンは接続が確立されているかどうかを明示的に制御することはできず、接続を介したデータフローの管理には使用できません。

単一の接続記述子は、トポロジ内の任意の2種類のピン間の接続を表すことができます。 接続の両側にあるピンは、フィルターでピン留めすることも、フィルター内のノードにピン留めすることもできます。また、接続には、一方の側にフィルターピンを設定し、もう一方の側にノードピンを設定することもできます。 ミニポートドライバーは、トポロジを接続記述子の配列として指定します。 1つの pin は複数の接続を持つことができます。つまり、同じ pin が配列内の複数の接続記述子に表示される可能性があります。

クライアントがミニポートドライバーから取得するトポロジの説明は、クライアントに認識されていないノードの種類を解釈する方法のオープンエンド検出をサポートするように設計されていません。 ノードの pin の番号付けだけでは、クライアントに pin の機能を検出するために必要な情報が提供されません。 ミニポートドライバーは、(GUID によって) ノードの種類を識別しますが、ノード型またはノード型でサポートされているピンを記述するパラメーターの標準化されたリストは提供しません。

たとえば、クライアントがノードタイプ GUID [**KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)を使用して自身を識別するノードを列挙した場合、クライアントは、ボリュームノードを処理するための規則を認識している場合にのみ、ノードを使用できます。 規則により、たとえば、ボリュームノードでは、 [**Ksk プロパティ\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)プロパティがサポートされ、ノードの pin 番号0と1が出力 (ソース) pin と入力 (シンク) ピンにそれぞれ割り当てられます。 さらに、ボリュームノードを制御できるクライアントは、通常、探索を比較的少数のノードの種類 (ボリュームおよびミュートノードなど) に制限する、ダイレクト検索を実行します。 クライアントでは、通常、ボリュームノードが含まれる可能性があるフィルターグラフの部分のみを探索します (たとえば、ミキサーの線)。

ミニポートインターフェイスでは、ミニポートドライバーからポートドライバーへの、要請されていない制御値の変更の配信がサポートされています。 この機能は、ユーザーが物理的に操作できるコントロールのノブ、スライダー、またはスイッチを備えたデバイスに対応します。 ユーザーがノードの制御値を変更するたびに、ハードウェアの割り込みによって、[ハードウェアイベント](hardware-events.md)が発生したことがポートドライバーに通知されます。

 

 




