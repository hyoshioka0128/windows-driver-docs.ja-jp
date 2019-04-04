---
title: オーディオのエンドポイント、プロパティおよびイベント
description: オーディオのエンドポイント、プロパティおよびイベント
ms.assetid: ffc5834f-30c8-40b5-b57b-fe784331690c
keywords:
- オーディオ イベント WDK
- WDK のオーディオのプロパティ
- ポート ドライバー WDK のオーディオ、プロパティ
- ポート ドライバー WDK のオーディオ、イベント
- アダプターのドライバー WDK のオーディオ、イベント
- アダプターのドライバー WDK のオーディオ、プロパティ
- オーディオのプロパティに関するプロパティ、WDK オーディオ
- オーディオのイベントについてイベント WDK、オーディオ
- WDM WDK オーディオのプロパティ
- WDM オーディオ イベント WDK
- WDM オーディオ プロパティ WDK、オーディオのプロパティについて
- KS プロパティ WDK オーディオ
- KS イベント WDK オーディオ
- WDK オーディオのプロパティ
- ピンの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27992b8952761b42a049e746ea329a2446297586
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551605"
---
# <a name="audio-endpoints-properties-and-events"></a>オーディオのエンドポイント、プロパティおよびイベント


## <span id="audio_properties_and_events"></span><span id="AUDIO_PROPERTIES_AND_EVENTS"></span>


PortCls システム ドライバーが記載されている組み込みの操作のサブセットをサポート[KS プロパティ、イベント、およびメソッド](https://msdn.microsoft.com/library/windows/hardware/ff567673)します。

Portcls.sys でポート ドライバーがサポートのいくつかのプロパティとイベントの要求ハンドラーを提供することで、ミニポート ドライバーのハンドラーには、他の要求を転送することによってプロパティおよびイベント。

WaveCyclic、WavePci、MIDI、および Dmu ポート ドライバーの現在の実装は、以下を説明します。

-   フィルター、pin、およびノードのプロパティのサポート

-   Pin とノード上のイベントのイベントをフィルターではなくサポート

クライアントは、プロパティまたはイベントの要求のターゲットとしてフィルターまたは暗証番号 (pin) のインスタンスへのハンドルを指定できます。 ノードのプロパティまたはイベントの要求では、フィルターまたは暗証番号 (pin) のハンドルだけでなく、ノード ID を指定します。 詳細については、[フィルター、Pin、およびノードのプロパティ](filter--pin--and-node-properties.md)を参照してください。

トポロジのポート ドライバーは次のよう

-   フィルターとそのノードのプロパティのサポート

-   ノード上のイベントのサポート

トポロジのフィルターのピンは、完全に存在し、したがってことはできませんをインスタンス化したり削除する有線接続を表します。

ポート ドライバーは、か、フィルターまたはそのピンとノード上のメソッドをサポートを提供します。 ポートのドライバーは、メソッドの要求を処理しないでくださいと、これらの要求を処理するためのミニポート ドライバーを転送しません。

オーディオのアダプターのドライバーでは、次の標準的なプロパティ セットの一部またはすべてをサポートします。

[KSPROPSETID\_AC3](https://msdn.microsoft.com/library/windows/hardware/ff537436)

[KSPROPSETID\_音響\_エコー\_キャンセル](https://msdn.microsoft.com/library/windows/hardware/ff537438)

[KSPROPSETID\_オーディオ](https://msdn.microsoft.com/library/windows/hardware/ff537440)

[KSPROPSETID\_DirectSound3DBuffer](https://msdn.microsoft.com/library/windows/hardware/ff537447)

[KSPROPSETID\_DirectSound3DListener](https://msdn.microsoft.com/library/windows/hardware/ff537449)

[KSPROPSETID\_DrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff537481)

[KSPROPSETID\_全般](https://msdn.microsoft.com/library/windows/hardware/ff566576)

[KSPROPSETID\_Hrtf3d](https://msdn.microsoft.com/library/windows/hardware/ff537482)

[KSPROPSETID\_ジャック](https://msdn.microsoft.com/library/windows/hardware/ff537484)

[KSPROPSETID\_暗証番号 (pin)](https://msdn.microsoft.com/library/windows/hardware/ff566584)

[KSPROPSETID\_シンセサイザー](https://msdn.microsoft.com/library/windows/hardware/ff537486)

[KSPROPSETID\_シンセサイザー\_Dls](https://msdn.microsoft.com/library/windows/hardware/ff537488)

[KSPROPSETID\_TopologyNode](https://msdn.microsoft.com/library/windows/hardware/ff537491)

すべてのオーディオ ドライバーのサポート、 **KSPROPSETID\_オーディオ**プロパティ セット。

オーディオのアダプターのドライバーによっては、次のイベント セットをサポートします。

[KSEVENTSETID\_AudioControlChange](https://msdn.microsoft.com/library/windows/hardware/ff537122)

さらに、オーディオのアダプターのドライバーは Ksmedia.h のヘッダー ファイルで定義されているその他のプロパティ セットのプロパティのハンドラーを提供する無料です。 ドライバーがまたを定義して独自のカスタム プロパティとイベントのセットをサポートしますが、カスタム プロパティまたはイベントについて認識しているアプリケーションのみが使用できます。

このセクションでは、オーディオ固有のプロパティとイベントについて説明します。 このガイドには、次のトピックがあります。

[オーディオのプロパティの要求](audio-property-requests.md)

[フィルター、Pin、およびノードのプロパティ](filter--pin--and-node-properties.md)

[オーディオのプロパティのハンドラー](audio-property-handlers.md)

[オーディオのプロパティに対する基本的なサポート クエリ](basic-support-queries-for-audio-properties.md)

[オーディオ エンドポイント ビルダー アルゴリズム](audio-endpoint-builder-algorithm.md)

[動的サブデバイス登録および登録解除](dynamic-subdeviceregistration-and-unregistration.md)

[マルチ チャネルのノードを公開します。](exposing-multichannel-nodes.md)

[暗証番号 (pin) カテゴリのプロパティ](pin-category-property.md)

[エンドポイントのオーディオ デバイスのフレンドリ名](friendly-names-for-audio-endpoint-devices.md)

[オーディオの位置プロパティ](audio-position-property.md)

[データ範囲は、プロパティの積集合をピン留め](pin-data-range-and-intersection-properties.md)

[Jack の Description プロパティ](jack-description-property.md)

[マイク配列 Geometry プロパティ](microphone-array-geometry-property.md)

[ハードウェア イベント](hardware-events.md)

 

 




