---
title: WavePci 遅延
description: WavePci 遅延
ms.assetid: 6d83c015-cf8f-40b4-bf28-de865a5bfe2d
keywords:
- WavePci 待機時間 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a72f3044ee389f55b43d1734a6e5786c28fa97d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829992"
---
# <a name="wavepci-latency"></a>WavePci 遅延


## <span id="wavepci_latency"></span><span id="WAVEPCI_LATENCY"></span>


WavePci port ドライバーは、WaveCyclic ドライバーとは異なる方法で、オーディオストリームのバッファー処理を行います。

WavePci ミニポートドライバーでハードウェアミックスが提供されている場合、DirectSound は、単一の循環バッファー内の DirectSound wave ストリーム全体を含む WavePci port ドライバーに IRP を送信します。 DirectSound は、仮想メモリの連続するブロックとしてバッファーを割り当てます。 DirectSound バッファーをコピーしないようにするために、カーネルストリーミングレイヤーはバッファーをカーネルモードの仮想メモリにマップし、循環バッファー内のメモリページの仮想アドレスと物理アドレスの両方を指定する MDL (メモリ記述子リスト) を生成します。 WavePci port ドライバーは、循環バッファーをアロケーターフレームのシーケンスに分割します (「 [KS アロケーター](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-allocators)」を参照してください)。 ミニポートドライバーは、ストリームの初期化中にポートドライバーによって[**IMiniportWavePciStream:: GetAllocatorFraming**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)メソッドが呼び出されたときに、推奨されるアロケーターフレームサイズを指定します。 ただし、システムグラフビルダーの SysAudio は、オーディオフィルターグラフ内の他のコンポーネントの要件を満たすために、ミニポートドライバーの設定を上書きできます。

WavePci port ドライバーは、循環バッファーを一連のマッピングとしてミニポートドライバーに公開します。 マッピングは、割り当てフレーム全体またはフレームの一部です。 特定の割り当てフレームがページ内に完全に存在する場合、ポートドライバーはそのフレームをミニポートドライバーに1つのマッピングとして提示します。 アロケーションフレームが1つまたは複数のページ境界をまたがっしている場合は、ポートドライバーによって各ページの境界にフレームが分割され、2つ以上のマッピングとして示されます。 [**Iportwavepcistream:: getmapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)を呼び出すたびに、シーケンス内で次の連続するマッピングが生成されます。

WaveCyclic の場合とは異なり、ミニポートドライバーは、ハードウェアでバッファーされるデータのミリ秒数をほとんど制御できません。 WavePci ミニポートドライバーは、いつでも開いているマッピングの数をかなり制御します。 オープンマッピングの数は、 [**Getmapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)を呼び出すたびに1ずつ増加し、 [**ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping)を呼び出すたびに1つずつ減少します。 (これにより、 **Getmapping**呼び出しは失敗する可能性があります。そのため、ドライバーはマッピングの数を全体的に制御するよりも少なくなります)。オープンマッピングの数を制御し、マッピングの累積サイズを追跡することによって、ミニポートドライバーは、ハードウェアが使用できるバッファーのミリ秒数を判断します (マッピングサイズに依存する許容範囲内)。 WavePci ミニポートドライバーは、許容されるレベルの枯渇を減らすために十分なページマッピングを要求する必要があります。

ミニポートドライバーが、読み取りポインターと書き込みポインターの間など、最大50ミリ秒のデータをバッファーに格納する場合、この制限はドライバーが累積するデータの最大量を表すことに注意してください。ただし、ストリームの待機時間に対するドライバーの影響。 ドライバーは、待機時間をできるだけ短く保つように設計する必要があります。 新しいストリームの再生を開始する前に、ミニポートドライバーが最初のマッピングセットを取得すると、ミニポートドライバーは、バッファー制限 (この例では50ミリ秒) に達するか、すぐにマッピングがなくなるまで、マッピングを要求し続けることができます。ご. ただし、後者の場合、ミニポートドライバーは、ストリームの再生を開始する前に、より多くのマッピングが使用可能になるまで待機することはできません。 代わりに、ドライバーは、既に取得したマッピングの再生をすぐに開始する必要があります。 後で、より多くのマッピングが使用可能になると、ドライバーは、バッファーサイズの制限に達するか、すぐに使用できるマッピングがなくなるまで、追加のマッピングを引き続き取得できます。

一般に、WavePci デバイスの DMA ハードウェアは、任意のバイトの配置で格納されているオーディオフレームに直接アクセスするように設計する必要があります。また、物理メモリの連続していないページ間で境界をまたがるします。 マッピングが整数のオーディオフレームであることを要求するデバイスがある場合、そのデバイスは、サポートされるオーディオ形式の種類に制限されます。 もちろん、この制限があるデバイスでは、2の累乗であるオーディオフレームサイズを引き続き処理できなければなりません。

たとえば、4つのチャネルと16ビットのサンプルサイズを持つデバイスには、8バイトのオーディオフレームサイズが必要です。 1つのページ (または8バイトの倍数であるその他の割り当てフレームのサイズ) 内では、非常に多くのオーディオフレームが適しています。 ただし、16ビットのサンプルを含む5.1 チャネルストリームの場合、オーディオフレームサイズは12バイトであり、1ページのサイズを超えるストリームには、ページ境界をまたがるするオーディオフレームが必ず含まれている必要があります。 ( [Wave フィルター](wave-filters.md)の図形はこの問題を示しています)。任意のバイトの配置と任意のバイト長のマッピングを処理できないハードウェアは、中間コピーを実行するためにドライバーに依存する必要があります。これにより、パフォーマンスが低下します。

Microsoft Windows Driver Kit (WDK) の Ac97 サンプルアダプタードライバーは、 [**Getallocatorframing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)メソッドを実装しています。 ミニポートドライバーは、このメソッドを使用して、優先されるフレーム割り当てサイズを通知します。 Windows 2000 および Windows Me では、出力ピンの上に[スプリッターシステムドライバー](kernel-mode-wdm-audio-components.md#splitter_system_driver) (スプリッター) がインスタンス化されている場合にのみ、ポートドライバーがこのメソッドを呼び出します。 Windows XP 以降では、ポートドライバーは入力ストリームに対してもこのメソッドを呼び出します。 SysAudio は、フレーム割り当てサイズを決定するときに、ミニポートドライバーの設定を無視することがあることに注意してください。

 

 




