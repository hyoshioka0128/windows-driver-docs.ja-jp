---
title: WaveCyclic 遅延
description: WaveCyclic 遅延
ms.assetid: 6de639c6-ddd5-4013-8d67-00731c328f47
keywords:
- WaveCyclic 待機時間の WDK オーディオ
- サイレント状態の間隔の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 772c43dd39488d1a02d00bac3b6b785b1d81f156
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364796"
---
# <a name="wavecyclic-latency"></a>WaveCyclic 遅延


## <span id="wavecyclic_latency"></span><span id="WAVECYCLIC_LATENCY"></span>


WaveCyclic ミニポート ドライバー、オーディオ再生のストリームが混在するとハードウェアを提供する場合、DirectSound は、1 つの循環バッファー DirectSound wave ストリーム全体を含む WaveCyclic ポート ドライバーは IRP を送信します。 WaveCyclic ポート ドライバーは IRP を受信し、フィード、波形データ--1 つずつの DMA バッファーには、ドライバーを公開するにします。 WaveCyclic が約 40 ミリ秒読み取りポインターの前、DMA バッファーの書き込みのポインターを保持しようとするとします。 ドライバーが DirectSound とハードウェアを行っている場合でも DMA バッファーで 40 ミリ秒余分なデータのあるか。

WaveCyclic ポート ドライバーが循環バッファー内のデータを最大 40 ミリ秒を蓄積するファクトでは、WaveCyclic ポート ドライバーは、ストリームの待機時間に 40 ミリ秒を追加することは限りません。 実際には、ポート、ドライバーは、ごくわずかな待機時間を追加します。 新しいストリームがポート ドライバーは循環バッファーの先頭に、初期データを書き込んでいる間に、再生が開始する前に、ポート ドライバーは、データが利用可能としているか、バッファーには、データの完全な 40 ミリ秒が含まれています。 まで書き込みを続行します。 ただし、すぐに利用できるこのデータ量よりも小さい場合は、ポート ドライバーではこの待機するミニポート ドライバーが強制されません。 代わりに、ミニポート ドライバー既にバッファー内のデータをすぐに再生を開始することができます。 後より多くのデータが使用可能なポート ドライバーには書き込みのいずれか以上のデータが利用可能になるまで、バッファーまたはデータの量にデータを読み取り間でバッファリングし、ポインターに達すると 40 ミリ秒の書き込みが続行されます。

ほぼスタベーションの期間の後に、サイレント状態の間隔が KMixer ストリームに含めることができます。 WaveCyclic は DMA バッファー内の余分なデータの 40 個ではなく 30 ミリ秒を維持するために KMixer から wave データだけを受信した、WaveCyclic は KMixer から有効なデータの最後に続く DMA バッファーへのサイレント状態の書き込みを開始します。 このポリシーによりスタベーションが発生し、デバイスが有効なデータの末尾を越えて読み取り、オーディオ デバイスが古い場合または初期化されていないデータではなくサイレント状態をレンダリングするようになります。

DMA バッファーに書き込まれた無音状態の量が非常に小さく、保持し、そのデータがバッファー内のサイレント状態を上書き KMixer silence 音声ガイダンスが再生された前に追加のデータと WaveCyclic ポート ドライバーを提供し、成功しますが場合、します。 不足がない場合は、オーディオ デバイスは、強制無音状態の間隔なしの混在のデータの連続ストリームを受信します。 ドライバーをデバッグするときにただし、表示もありますミニポート ドライバーの[ **IMiniportWaveCyclicStream::Silence** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-silence)場合でも、オーディオ、レンダラーの不足が呼び出されるメソッド。

 

 




