---
title: トポロジ ポート ドライバー
description: トポロジ ポート ドライバー
ms.assetid: f671f557-552e-4575-babf-869c8c0b8f08
keywords:
- トポロジ ポート ドライバー WDK オーディオ
- PortCls WDK のオーディオ、ポートのドライバー
- オーディオのミニポート ドライバー WDK、ポート ドライバー
- ミニポート ドライバー WDK のオーディオ、ポートのドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39dcdfd03361c868d38b2cb794c10a25d72f8cb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328540"
---
# <a name="topology-port-driver"></a>トポロジ ポート ドライバー


## <span id="topology_port_driver"></span><span id="TOPOLOGY_PORT_DRIVER"></span>


トポロジのポート ドライバー公開オーディオのアダプターのトポロジのハードウェアを混在させます。 たとえば、wave レンダラーと通常のアダプターで MIDI シンセサイザーから再生ストリームが混在するハードウェアは、コントロールのノード (ボリューム、ミュート、および合計) と、ノードを接続するデータ パスのセットとしてモデル化できます。 このトポロジは、一連のコントロールとミキサー行として Windows のマルチ メディア ミキサー API によって公開される (を参照してください[オーディオ Mixer API 翻訳にカーネル ストリーミング トポロジ](kernel-streaming-topology-to-audio-mixer-api-translation.md))。 アダプターのドライバーは、対応する[トポロジ ミニポート ドライバー](topology-miniport-driver.md)トポロジ ポート ドライバーはフォームをバインドする、[トポロジ フィルター](topology-filters.md)。

トポロジのポートのドライバーを公開して、 [IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)ミニポート ドライバーへのインターフェイス。 IPortTopology 基底インターフェイスからメソッドを継承する[IPort](https://msdn.microsoft.com/library/windows/hardware/ff536842); 追加のメソッドを備えていません。

トポロジのポートおよびミニポート ドライバー オブジェクトが、それぞれを相互通信[IPortTopology](https://msdn.microsoft.com/library/windows/hardware/ff536896)と[IMiniportTopology](https://msdn.microsoft.com/library/windows/hardware/ff536712)インターフェイス。

 

 




