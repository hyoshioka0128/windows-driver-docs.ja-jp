---
title: トポロジ ポート ドライバー
description: トポロジ ポート ドライバー
ms.assetid: f671f557-552e-4575-babf-869c8c0b8f08
keywords:
- トポロジポートドライバー WDK オーディオ
- PortCls WDK オーディオ、ポートドライバー
- オーディオミニポートドライバー WDK、ポートドライバー
- ミニポートドライバー WDK オーディオ、ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78afd447dd12d56bacaa5e564791245a373c8fd2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829989"
---
# <a name="topology-port-driver"></a>トポロジ ポート ドライバー


## <span id="topology_port_driver"></span><span id="TOPOLOGY_PORT_DRIVER"></span>


トポロジポートドライバーは、オーディオアダプターの混合ハードウェアのトポロジを公開します。 たとえば、一般的なアダプターの wave レンダラーと MIDI シンセサイザーからの再生ストリームをミックスするハードウェアは、一連の制御ノード (ボリューム、ミュート、および合計) に加えて、ノードを接続するデータパスをモデル化することができます。 このトポロジは、Windows マルチメディアミキサー API (「[カーネルストリーミングトポロジからオーディオミキサー api への変換」を](kernel-streaming-topology-to-audio-mixer-api-translation.md)参照) によって、一連のコントロールとミキサーラインとして公開されます。 アダプタードライバーには、トポロジポートドライバーにバインドして[トポロジフィルター](topology-filters.md)を形成する、対応する[トポロジミニポートドライバー](topology-miniport-driver.md)が用意されています。

トポロジポートドライバーは、ミニポートドライバーに[Iporttopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)インターフェイスを公開します。 IPortTopology は、基本インターフェイス[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)からメソッドを継承します。追加のメソッドはありません。

トポロジポートとミニポートドライバーオブジェクトは、それぞれの[Iporttopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iporttopology)インターフェイスと[IMiniportTopology](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiporttopology)インターフェイスを介して相互に通信します。

 

 




