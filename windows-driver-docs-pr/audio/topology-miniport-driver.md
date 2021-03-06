---
title: トポロジ ミニポート ドライバー
description: トポロジ ミニポート ドライバー
ms.assetid: 3e0b797e-2fa5-499b-a465-0f51f5433177
keywords:
- オーディオのミニポート ドライバー WDK、トポロジ
- ミニポート ドライバー WDK オーディオのトポロジ
- トポロジのミニポート ドライバー WDK オーディオ
- トポロジ ミニポート インターフェイス WDK オーディオ
- 接続記述子 WDK オーディオ
- ノードから WDK オーディオ
- ノードの WDK オーディオ
- 識別ノード識別子 WDK オーディオ
- オーディオの WDK の混在
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ac4010e1c670444bb24f68e64809871cdf9068d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354184"
---
# <a name="topology-miniport-driver"></a>トポロジ ミニポート ドライバー


## <span id="topology_miniport_driver"></span><span id="TOPOLOGY_MINIPORT_DRIVER"></span>


トポロジのミニポート ドライバーでは、アダプターのオーディオ ミキサー回路で、さまざまなハードウェア コントロール (たとえば、ボリュームおよびミュート) を管理します。 このドライバーとしてコントロールを列挙する*ノード*ミキサー トポロジでは、クライアントをできるように、ノード間の相互接続を検出してクエリを実行し、各ノードで制御するパラメーターを設定します。

[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)を構築するときに、アダプターのトポロジでは、[オーディオ フィルター グラフ](audio-filter-graphs.md)します。 ミキサー API (Microsoft Windows sdk の Windows のマルチ メディア セクションで説明) は、ミキサー行の制御し、SndVol32 などのユーザー モード アプリケーションを許すことに、トポロジのノードを表します。 詳細については、次を参照してください。[システム トレイと SndVol32](systray-and-sndvol32.md)します。

トポロジのミニポート ドライバーには、ミニポート ドライバーを初期化するために、ポートのドライバーを使用する、トポロジのミニポート インターフェイスを実装する必要があります。 ミニポート インターフェイス[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiporttopology)でメソッドを継承、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)インターフェイスです。 追加のメソッドを備えていません。 オーディオのアダプターのドライバー フォーム、[トポロジ フィルター](topology-filters.md)ミニポート オブジェクトの IMiniportTopology をバインドすることによって、ポート オブジェクトのインターフェイス[IPortTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iporttopology)インターフェイス。

通常、トポロジのフィルターにはアダプター内の他のデバイスが他にもトポロジ ノードを含めることができますが、ほとんどアダプターのトポロジのノードにはが含まれます。 たとえば、wave フィルターとして表される、wave デバイスが DAC を含めることが ([**KSNODETYPE\_DAC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-dac)) と ADC ([**KSNODETYPE\_ADC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-adc)) ノードです。

クエリを実行して、トポロジのノード上のコントロール パラメーターの設定は、プロパティの要求によって実行されます。 各ノードの種類は、特定のプロパティまたはプロパティのセットに関連付けられます。 ノードには、1 つだけのコントロールの値がサポートされます。 たとえば、ボリュームのノード ([**KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume))、現在の音量の設定を示す値を持ちます。 他のノードには、複数のコントロールの値がサポートされます。 たとえば、3 D ノード ([**KSNODETYPE\_3D\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)) さまざまな 3D バッファーと 3D のリスナーのプロパティをサポートしています。 合計ノード ([**KSNODETYPE\_合計**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-sum))、その一方で、コントロールの値がありません。

トポロジのミニポート ドライバーを使用して、*接続記述子*([**PCCONNECTION\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))) に 2 つのトポロジのノード間の接続について説明します。 各接続が転送されからノードとするノードの両方を指定します。 ノードがいくつかの pin を必要があり、他のピンの 1 つの pin によって実行される関数が異なる場合があります。 別の 1 つの pin を区別するために、ミニポート ドライバー ノードで、ピンを数値します。 接続記述子に、これらのピン番号が表示されます。 たとえば、状態変数のフィルターには、次の 3 つの出力ピン - 高の 1 つずつ、middle、および低周波数の番号 1、2、および 3 が付けられますがあります。 ピン番号に関連付けられているピンする接続を確認するミニポート ドライバーのクライアントが使用できます。

接続記述子を使用して、*ノード識別子を識別*、 [ **PCFILTER\_ノード**](https://docs.microsoft.com/previous-versions/ff537695(v=vs.85))、内のノードで pin からフィルターで pin を区別するために、フィルターです。 各オーディオのアダプターでオーディオのレンダリングとキャプチャ デバイスにミキサー回路の有線接続は、トポロジのフィルターに暗証番号 (pin) として表されます。 他のトポロジ フィルター ピンは、アダプター カードのライン出力ジャックなど、外部の物理接続を表します。 トポロジのフィルターのピンは、物理、アダプターのハードウェアの有線接続を表します。 したがって、ピンに接続が確立するかどうかを明示的に制御を提供できませんし、その接続経由でのデータ フローを管理するのには使用できません。

1 つの接続記述子では、トポロジ内の 2 つの pin 型間の接続を記述できます。 接続の両側でピン両方フィルターで pin や、フィルター内のノードでピンでもかまいませんの接続は、一方の側でフィルター pin と、他のノードの pin を持つことができます。 ミニポート ドライバーでは、接続記述子の配列としてのトポロジを指定します。 ピンが 1 つは、1 つ以上の接続を同じ pin が配列内の 1 つ以上の接続記述子で表示できることを意味を持つことができます。

ミニポート ドライバーからクライアントを取得するトポロジの説明は、クライアントに不明なノード型を解釈する方法の拡張可能な探索をサポートするために設計されていません。 ノード ピン番号だけでは、クライアントは、ピンの機能の検出に必要な情報を提供しません。 ミニポート ドライバーでは、ノードの型を識別します (GUID) を使用して、標準化されたパラメーターの一覧、ノードの種類またはノードの種類でサポートされている pin のいずれかを記述するためは提供されません。

たとえば、クライアントは、ノードを列挙します使用する場合はノードの種類の GUID [ **KSNODETYPE\_ボリューム**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)自体を識別するには、するには、クライアント設定の規則がわかっている場合にのみ、ノードの使用。ボリュームのノードを処理します。 慣例により、ボリュームのノード、たとえば、サポート、 [ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)プロパティと出力 (ソース) の暗証番号 (pin) へのノード ピン番号 0 と 1 を代入し、(シンク) の暗証番号 (pin) をそれぞれ入力します。 さらに、通常は、[ボリューム] ノードを制御できるクライアントは、比較的少数のノードの種類 (ボリュームとミュート ノード、たとえば) にその探索を制限する自律的な検索を実行します。 通常、クライアントには、ボリューム ノード (たとえば、ミキサー行) を格納する可能性のあるフィルター グラフの部分のみがについて説明します。

ミニポート インターフェイスには、ミニポート ドライバーからポート ドライバーへの要請されていないコントロール値の変更の配信がサポートしています。 この機能には、コントロールのノブ、スライダー、またはユーザーが物理的に操作できるスイッチを持つデバイスが対応しています。 ノードのコントロールの値を変更するたび、ハードウェア割り込みポート ドライバーに通知する、[ハードウェア イベント](hardware-events.md)が発生しました。

 

 




