---
title: WaveCyclic 遅延
description: WaveCyclic 遅延
ms.assetid: 6de639c6-ddd5-4013-8d67-00731c328f47
keywords:
- WaveCyclic 待機時間 WDK オーディオ
- 無音期間 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bd9f31912c7f9479a6c00643c5f304f93993613
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833765"
---
# <a name="wavecyclic-latency"></a>WaveCyclic 遅延


## <span id="wavecyclic_latency"></span><span id="WAVECYCLIC_LATENCY"></span>


WaveCyclic ミニポートドライバーがオーディオ再生ストリームのハードウェアミックスを提供する場合、DirectSound は、単一の循環バッファー内の DirectSound wave ストリーム全体を含む WaveCyclic port ドライバーに IRP を送信します。 WaveCyclic port ドライバーは、IRP を受信し、ドライバーが公開する DMA バッファーに wave データを分割します。 WaveCyclic は、読み取りポインターの前に、DMA バッファーの書き込みポインターを40ミリ秒前後に保持しようとします。 ドライバーが DirectSound とハードウェアの混合を行っている場合でも、DMA バッファーに余分なデータが約40ミリ秒かかることが予想されます。

WaveCyclic port ドライバーは、循環バッファーに最大40ミリ秒のデータを蓄積しようとするのではなく、WaveCyclic port ドライバーがストリームの待機時間に40ミリ秒を加算するという意味ではありません。 実際、ポートドライバーの待機時間はごくわずかです。 新しいストリームが再生を開始する直前に、ポートドライバーが最初のデータを循環バッファーの先頭に書き込んでいる間、ポートドライバーは、データが使用できなくなるか、バッファーに完全な40ミリ秒のデータが格納されるまで書き込みを続けます。 ただし、このデータ量よりも少ない場合は、ポートドライバーによってミニポートドライバーが強制的に待機することはありません。 代わりに、ミニポートドライバーは、既にバッファリングされているデータの再生をすぐに開始できます。 その後、より多くのデータが使用可能になると、ポートドライバーは、データが使用できなくなるか、読み取りポインターと書き込みポインター間でバッファーされるデータ量が40ミリ秒になるまで、データをバッファーに書き込み続けます。

近い期間が経過すると、KMixer ストリームに無音の間隔を含めることができます。 WaveCyclic が KMixer から十分な数の wave データのみを受信し、DMA バッファーに余分なデータが40ミリ秒で保持される場合、WaveCyclic は KMixer からの有効なデータの末尾に達したときに、DMA バッファーに無音の書き込みを開始します。 このポリシーにより、枯渇が発生し、デバイスが有効なデータの末尾を越えて読み取られた場合に、古いデータや初期化されていないデータではなく、無音状態がレンダリングされます。

DMA バッファーに書き込まれたサイレント状態のサイズはかなり小さくなります。また、サイレント状態が再生される前に、KMixer が WaveCyclic port ドライバーに追加データを指定して成功した場合、そのデータはバッファー内の無音を上書きします。 枯渇がない場合、オーディオデバイスは、強制されていない無音の間隔なしに、混合データの連続ストリームを受信します。 ただし、ドライバーをデバッグしているときに、オーディオレンダラーが不足していない場合でも、ミニポートドライバーの[**IMiniportWaveCyclicStream:: 沈黙**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-silence)メソッドが呼び出されている可能性があります。

 

 




