---
title: WavePci 遅延
description: WavePci 遅延
ms.assetid: 6d83c015-cf8f-40b4-bf28-de865a5bfe2d
keywords:
- WavePci 待機時間の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4124c40c4374711872759edc36aee92d31662679
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354129"
---
# <a name="wavepci-latency"></a>WavePci 遅延


## <span id="wavepci_latency"></span><span id="WAVEPCI_LATENCY"></span>


WavePci ポート ドライバーでは、異なる WaveCyclic ドライバーからオーディオ ストリームのバッファリングを処理します。

WavePci ミニポート ドライバーでは、ハードウェアの混在を提供する場合、DirectSound は、1 つの循環バッファー DirectSound wave ストリーム全体を含む WavePci ポート ドライバーは IRP を送信します。 DirectSound は、仮想メモリの連続するブロックとバッファーを割り当てます。 DirectSound バッファーのコピーを回避するには、は、カーネル ストリーミング レイヤーは、カーネル モードの仮想メモリにバッファーをマップし、循環バッファーのメモリ ページの仮想および物理アドレスの両方を指定する MDL (メモリ記述子のリスト) を生成します。 WavePci ポート ドライバーは、アロケーターのフレームのシーケンスに循環バッファーをパーティション分割 (を参照してください[KS アロケーター](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-allocators))。 ミニポート ドライバーがその優先アロケーター フレームを指定する場合のサイズ、 [ **IMiniportWavePciStream::GetAllocatorFraming** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)メソッドは、ストリームの初期化中に、ポート ドライバーによって呼び出されます。 ただし、SysAudio、システムのグラフ ビルダーには、オーディオ フィルター グラフ内の他のコンポーネントの要件に対応するために、ミニポート ドライバーの設定をオーバーライドできます。

WavePci ポート ドライバーでは、マッピングのシーケンスとしてミニポート ドライバーに循環バッファーを公開します。 マッピングは、全体の割り当てフレームまたはフレームの一部です。 特定の割り当てのフレームがページ内に完全に、ポート ドライバー マッピングは 1 つとして、ミニポート ドライバーには、そのフレームに表示されます。 場合は、割り当てフレームは、1 つまたは複数のページ境界をまたぐ、ポート ドライバーは各ページの境界にフレームを分割し、2 つ以上のマッピングとして提示します。 呼び出しごとに[ **IPortWavePciStream::GetMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping)シーケンス内の次の連続するマッピングを生成します。

WaveCyclic 場合、場所、ミニポート ドライバーでは、データの時間をミリ秒単位では、ハードウェアでバッファーを制御するほとんどとは対照的 WavePci ミニポート ドライバーは、いつでも開くことがマッピングの数を細かく制御ができます。 開いているマッピングの数が呼び出しごとに 1 つずつ増加[ **GetMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping)し呼び出しごとに 1 つ減少[ **ReleaseMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-releasemapping). (A **GetMapping**呼び出しが失敗する、もちろん、ドライバーがある完全に制御のマッピングの数より小さいためです)。オープン マッピングの数の制御と、累積的なを追跡することによって、マッピングのサイズ ミニポート ドライバーが判断できます (マップのサイズに依存する許容範囲) 内のバッファリングのミリ秒数、ハードウェアを使用できます。 WavePci ミニポート ドライバーでは、許容できるレベルに枯渇の可能性を低減するための十分なページ マッピングを要求する必要があります。

場合ミニポート ドライバーのポリシーは、データの最大 50 ミリ秒をバッファーには、たとえば、読み取りと書き込みのポインター間に注意してこの制限が、ドライバーが累積されますが、しませんし、表す必要がありますいないデータの上限を表すこと、ストリームの待機時間にドライバーのコントリビューション。 その待機時間をできるだけ小さく維持するには、ドライバーを設計する必要があります。 ミニポート ドライバーでは、新しいストリームの再生を開始する前に、初期のマッピングのセットを取得するミニポート ドライバーは、そのバッファーの制限 (この例では 50 ミリ秒単位) に達するかまたは複数のマッピングがありませんがすぐになるまでのマッピングを要求を続行できます。ご利用いただけます。 後者の場合、ただし、ミニポート ドライバー待つ必要がありますいないストリームの再生を開始する前に、複数のマッピングが使用可能になります。 代わりに、ドライバーすぐに再生を開始するマッピングが既に取得しています。 後で、複数のマッピングが使用可能になると、ドライバーは、バッファー サイズの制限に達するか、または複数のマッピングがありませんがすぐに利用できるまで、その他のマッピングを取得を続行できます。

一般に、WavePci デバイスの DMA のハードウェアの場合は、任意のバイト アラインメントに格納されていると、物理メモリの非連続のページ間の境界をまたがるをオーディオ フレームに直接アクセスするように設計する必要があります。 マッピングは、オーディオ フレーム数が整数である必要がありますデバイスがあれば、そのデバイスでサポートされるオーディオ形式の種類に制限されます。 もちろん、この制限を使用したデバイスは、2 の累乗であるオーディオ フレーム サイズを処理できる必要があります。

たとえば、4 つのチャネルと、16 ビットのサンプル サイズを使用したデバイスには、8 バイトのオーディオ フレーム サイズを取得が必要です。 オーディオ フレーム数が整数にページ (または 8 バイトの倍数であるその他の割り当てフレーム サイズ) きちんと収まります。 ただし、16 ビットのサンプルを使って、5.1 チャネル ストリームの場合に、オーディオ フレーム サイズは 12 バイト、ストリーム必ずしも 1 つのページのサイズを超えるにはページ境界をまたがるオーディオ フレームが含まれています。 (図では、 [Wave フィルター](wave-filters.md)この問題を示しています)。任意のバイト アラインメントと任意のバイト長のマッピングを処理できないハードウェアは必要があります、パフォーマンスが低下する中間コピーを実行するドライバーに依存します。

Ac97 サンプル アダプタのドライバで、Microsoft Windows Driver Kit (WDK) の実装を[ **GetAllocatorFraming** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)メソッド。 ミニポート ドライバーでは、このメソッドを使用して、その最適なフレーム割り当てサイズを通信します。 Windows 2000 と Windows Me、ポート、ドライバーはこのメソッドを呼び出して場合にのみ、[スプリッター システム ドライバー](kernel-mode-wdm-audio-components.md#splitter_system_driver) (Splitter.sys) が、出力ピンの上にインスタンス化します。 Windows XP 以降では、ポート、ドライバーは、入力ストリームものこのメソッドを呼び出します。 SysAudio フレーム割り当てサイズを決定するときに、ミニポート ドライバーの設定を無視する選択することに注意してください。

 

 




