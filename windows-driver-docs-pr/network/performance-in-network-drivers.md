---
title: ネットワークドライバーのパフォーマンス
description: ここでは、ネットワークドライバーのパフォーマンスを向上させる方法について説明します。
ms.assetid: 7EA23AA6-7673-4D88-91CA-BDDD8FBB2A4F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0c6969026a82a98bc7ecc95ef11d04b96c2e159
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843693"
---
# <a name="performance-in-network-drivers"></a>ネットワーク ドライバーのパフォーマンス


-   [送信と受信のパスの長さを最小限にする](#minimizing-send-and-receive-path-length)
-   [プロセッサ間の共有を最小限にするためにデータとコードをパーティション分割する](#partitioning-data-and-code-to-minimize-sharing-across-processors)
-   [偽共有の回避](#avoiding-false-sharing)
-   [ロックメカニズムを適切に使用する](#using-locking-mechanisms-properly)
-   [64ビット DMA の使用](#using-64-bit-dma)
-   [適切なバッファーの配置を保証する](#ensuring-proper-buffer-alignment)
-   [スキャッター/ギャザー DMA の使用](#using-scatter-gather-dma)
-   [受信側スロットルのサポート](#supporting-receive-side-throttle)

## <a name="minimizing-send-and-receive-path-length"></a>送信と受信のパスの長さを最小限にする


送信パスと受信パスはドライバーによって異なりますが、パフォーマンスの最適化にはいくつかの一般的な規則があります。

-   共通パスを最適化します。 Kernprof ツールは、必要な情報を抽出する Windows の developer および IDW ビルドに付属しています。 開発者は、最も CPU サイクルを消費するルーチンを調べて、これらのルーチンが呼び出される頻度や、これらのルーチンで費やされた時間を減らす必要があります。

-   ネットワークアダプタードライバーが過剰なシステムリソースを使用せず、システム全体のパフォーマンスが低下するように、DPC に費やされた時間を短縮します。

-   デバッグコードが最終的にリリースされたバージョンのドライバーにコンパイルされていないことを確認します。これにより、余分なコードの実行を回避できます。

## <a name="partitioning-data-and-code-to-minimize-sharing-across-processors"></a>プロセッサ間の共有を最小限にするためにデータとコードをパーティション分割する


プロセッサ間で共有データとコードを最小限に抑えるには、パーティション分割が必要です。 パーティション分割によって、システムバスの使用率が軽減され、プロセッサキャッシュの有効性が向上します。 共有を最小限にするために、ドライバーの作成者は次の点を考慮する必要があります。

-   「[逆シリアル化された NDIS ミニポートドライバー](deserialized-ndis-miniport-drivers.md)」で説明されているように、ドライバーを逆シリアル化して実装します。

-   プロセッサごとのデータ構造を使用して、グローバルおよび共有データへのアクセスを減らします。 これにより、統計カウンターを同期なしで保持することができます。これにより、コードのパスの長さが短縮され、パフォーマンスが向上します。 重要な統計情報については、クエリ時に加算されるプロセッサごとのカウンターがあります。 グローバルカウンターが必要な場合は、カウンターを操作するためにスピンロックではなく、インタロックされた操作を使用します。 スピンロックの使用を回避する方法については、以下の「ロックメカニズムの使用」を参照してください。

    これを容易にするために、 [**Kegetcurrentprocessornumber ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kegetcurrentprocessornumberex)を使用して現在のプロセッサを特定できます。 プロセッサごとのデータ構造を割り当てるときのプロセッサ数を決定するために、 [**KeQueryGroupAffinity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequerygroupaffinity)を使用できます。

    Affinity mask に設定されているビットの合計数は、システム内のアクティブなプロセッサの数を示します。 オペレーティングシステムの将来のリリースでは、プロセッサに連続した番号が付けられていない可能性があるため、ドライバーはマスク内のすべてのセットビットが連続していると想定しないでください。 SMP マシンのプロセッサ数は、0から始まる値です。

    ドライバーがプロセッサごとのデータを保持している場合は、 [**KeQueryGroupAffinity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kequerygroupaffinity)関数を使用して、キャッシュラインの競合を減らすことができます。

## <a name="avoiding-false-sharing"></a>偽共有の回避


偽共有は、プロセッサが互いに独立している共有変数を要求するときに発生します。 ただし、変数は同じキャッシュラインにあるため、プロセッサ間で共有されます。 このような状況では、キャッシュラインは、その中の変数のいずれかにアクセスするたびにプロセッサ間を行き来して、キャッシュのフラッシュと再読み込みの増加を引き起こします。 これにより、システムバスの使用率が増加し、システム全体のパフォーマンスが低下します。

偽共有を回避するには、 [**NdisGetSharedDataAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetshareddataalignment)を使用して、重要なデータ構造 (スピンロック、バッファーキューヘッダー、単一リンクリストなど) をキャッシュ行の境界に揃えます。

## <a name="using-locking-mechanisms-properly"></a>ロックメカニズムを適切に使用する


スピンロックは、適切に使用しないとパフォーマンスを低下させる可能性があります。 ドライバーは、可能な限りインタロックされた操作を使用することによって、スピンロックの使用を最小限に抑えます。 ただし、場合によっては、一部の目的では、スピンロックが最適な選択肢となることがあります。 たとえば、ドライバーがドライバーに戻されていないパケットの数の参照カウントを処理するときに、ドライバーがスピンロックを取得した場合、インタロックされた操作を使用する必要はありません。 詳細については、「[ネットワークドライバーでの同期と通知](synchronization-and-notification-in-network-drivers.md)」を参照してください。

ロックメカニズムを効果的に使用するためのヒントを次に示します。

-   リソースプールの管理には、次のような NDIS シングルリンクリスト関数を使用します。

    [**NdisInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinitializeslisthead)

    [**NdisInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockedpushentryslist)

    [**NdisInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisinterlockedpopentryslist)

    [**NdisQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerydepthslist)

-   スピンロックを使用する必要がある場合は、コードではなく、データを保護するために使用します。 共通パスで使用されるすべてのデータを保護するために1つのロックを使用しないでください。 たとえば、送信パスと受信パスで使用されるデータを2つのデータ構造に分割し、送信パスでデータをロックする必要がある場合、受信パスは影響を受けません。

-   スピンロックを使用していて、パスが既に DPC レベルにある場合は、 [**NdisDprAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock)関数と[**NdisDprReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdprreleasespinlock)関数を使用して、ロックを取得して解放するときに余分なコードを使用しないようにします。

-   スピンロックの取得と解放の回数を最小限に抑えるには、次の NDIS RWLock 関数を使用します。

    [**NdisAllocateRWLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocaterwlock)

    [**NdisAcquireRWLockRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirerwlockread)

    [**NdisAcquireRWLockWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirerwlockwrite)

    [**NdisReleaseRWLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleaserwlock)

## <a name="using-64-bit-dma"></a>64ビット DMA の使用


64-ビット DMA ネットワークアダプターが64ビット DMA をサポートしている場合は、4 GB の範囲を超えるアドレスの余分なコピーを回避するための手順を実行する必要があります。 ドライバーが[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)を呼び出すと、 **NDIS\_SG\_DMA\_64\_ビット\_アドレス**フラグが*Flags*パラメーターに設定されている必要があります。

## <a name="ensuring-proper-buffer-alignment"></a>適切なバッファーの配置を保証する


キャッシュライン境界でのバッファーの配置により、あるバッファーから別のバッファーにデータをコピーするときのパフォーマンスが向上します。 ほとんどのネットワークアダプターの受信バッファーは、最初に割り当てられるときに適切にアラインされますが、最終的にアプリケーションバッファーにコピーする必要があるユーザーデータは、使用されているヘッダー領域によって不整合になります。 TCP データ (最も一般的なシナリオ) の場合、TCP、IP、およびイーサネットのヘッダーによるシフトは、0x36 バイトのシフトになります。 この問題を解決するには、ドライバーが少し大きなバッファーを割り当て、0xA バイトのオフセットでパケットデータを挿入することをお勧めします。 これにより、バッファーがヘッダーに対して0x36 バイトずつシフトされた後、ユーザーデータが適切にアラインされるようになります。 キャッシュラインの境界の詳細については、 [**NdisMAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)の「解説」を参照してください。

## <a name="using-scatter-gather-dma"></a>スキャッター/ギャザー DMA の使用


[NDIS スキャッター/ギャザー DMA](ndis-scatter-gather-dma.md)は、物理メモリの連続していない範囲との間でのデータ転送をサポートするハードウェアを提供します。 スキャッター/ギャザー DMA では、散布図[ **\_gather\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_scatter_gather_list)構造体が使用されます。これには、\_要素の構造と配列内の要素の数を**集めた散布\_** の配列が含まれます。 この構造体は、ドライバーの send 関数に渡されるパケット記述子から取得されます。 配列の各要素は、物理的に連続するスキャッター/ギャザー領域の長さと開始物理アドレスを提供します。 ドライバーは、データを転送するための長さとアドレス情報を使用します。

DMA 操作にスキャッター/ギャザールーチンを使用すると、マップレジスタが使用された場合に発生するように、これらのリソースを静的にロックせずに、システムリソースの使用率を向上させることができます。 詳細については、「 [NDIS スキャッター/GATHER DMA](ndis-scatter-gather-dma.md)」を参照してください。

ネットワークアダプターが TCP セグメント化オフロード (大規模な送信オフロード) をサポートしている場合、ドライバーは、 [**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)関数内の*maximumphysicalmapping*パラメーターに、tcp/ip から取得できる最大バッファーサイズを渡す必要があります。 これにより、ドライバーには、スキャッター/ギャザーリストを構築するための十分なマップレジスタがあることが保証され、バッファーの割り当てとコピーが可能になります。 詳しくは、次のトピックをご覧ください。

- [タスクオフロード機能の決定](determining-task-offload-capabilities.md)
- [大きな TCP パケットのセグメント化のオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

## <a name="supporting-receive-side-throttle"></a>受信側スロットルのサポート


マルチメディアアプリケーションでメディアの再生中の中断を最小限に抑えるには、NDIS 6.20 以降のドライバーで受信割り込みを処理するときの Receive Side スロットル (RST) がサポートされている必要があります。 詳しくは、次のトピックをご覧ください。

[NDIS 6.20 での Receive Side スロットル](receive-side-throttle-in-ndis-6-20.md)[ミニポートドライバーを NDIS 6.20 に移植するために必要な変更の概要](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-20.md)に関する「コードパスの送信と受信」
 

 





