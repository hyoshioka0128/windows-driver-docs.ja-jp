---
title: WaveRT ポート ドライバーの概要
description: WaveRT ポート ドライバーの概要
ms.assetid: 48b2b59e-385e-4814-ac20-c4b1a08f32dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc75496a8214bf76fb258ddac31b334ccbd46050
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831152"
---
# <a name="introducing-the-wavert-port-driver"></a>WaveRT ポート ドライバーの概要


Windows Vista 以降のオペレーティングシステムでは、パフォーマンスの向上を実現しますが、オーディオストリームのレンダリングとキャプチャに単純な循環バッファーを使用する、wave リアルタイム (WaveRT) ポートドライバーのサポートが提供されています。

WaveRT ポートドライバーのパフォーマンスが向上すると、次のような特性があります。

-   Wave キャプチャと wave レンダリング中の低待機時間

-   耐障害性を備えたオーディオストリーム

以前のバージョンの Microsoft Windows の WaveCyclic および WavePci port ドライバーと同様に、WaveRT ポートドライバーは、[カーネルストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/kernel-streaming)(KS) フィルターの一般的な機能を提供します。 WaveRT ポートドライバーでは、次の操作を実行できるオーディオデバイスがサポートされています。

-   PCI Express bus などのシステムバスに接続できます。

-   Wave データ ( [**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)または[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)構造体で記述されたオーディオデータ) を再生または録音できます。

-   Windows Vista では、オーディオストリームの待機時間を短縮するために、強化されたスケジュールサポートを利用できます。

オーディオデバイスが Windows で提供されるオーディオの機能強化を利用できるようにするには、オーディオデバイスがストリーミング中にドライバーソフトウェアによる操作をほとんどまたはまったく行わずに、オーディオデータを再生またはキャプチャできる必要があります。 WaveRT ポートドライバーを使用する適切に設計されたオーディオデバイスでは、オーディオストリームがその状態から抜けるまで、オーディオストリームが*実行*状態になるまでに、ドライバーソフトウェアのヘルプをほとんどまたはまったく必要としません。

WaveRT ポートドライバーの主なクライアントは、共有モードで実行されるオーディオエンジンです。 Windows Vista オーディオエンジンの詳細については、「 [Windows Vista オーディオエンジンの](exploring-the-windows-vista-audio-engine.md)操作」を参照してください。

 

 




