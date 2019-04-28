---
title: ネットワークのドライバーでのパフォーマンス
description: このセクションは、ネットワーク ドライバーのパフォーマンスを向上するための手法を説明します
ms.assetid: 7EA23AA6-7673-4D88-91CA-BDDD8FBB2A4F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b81cd924da99bb167dc65ad39783fead6f0c5765
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366690"
---
# <a name="performance-in-network-drivers"></a>ネットワーク ドライバーのパフォーマンス


-   [送信を最小限に抑えることと、パスの長さを受け取る](#minimizing-send-and-receive-path-length)
-   [データとを最小限に抑えるプロセッサ間で共有コードをパーティション分割](#partitioning-data-and-code-to-minimize-sharing-across-processors)
-   [偽共有の回避](#avoiding-false-sharing)
-   [ロック メカニズムを正しく使用します。](#using-locking-mechanisms-properly)
-   [64 ビットの DMA を使用してください。](#using-64-bit-dma)
-   [適切なバッファーのアライメントを確保します。](#ensuring-proper-buffer-alignment)
-   [スキャッター/ギャザー DMA を使用します。](#using-scatter-gather-dma)
-   [受信側のスロットルのサポート](#supporting-receive-side-throttle)

## <a name="minimizing-send-and-receive-path-length"></a>送信を最小限に抑えることと、パスの長さを受け取る


送信と受信パスにドライバーが異なる場合、パフォーマンスの最適化のいくつかの一般的な規則があります。

-   一般的なパスを最適化します。 Kernprof.exe ツールは、開発者に付属し、必要な情報を抽出する Windows のビルドに使用します。 開発者は、ほとんどの CPU サイクルを消費し、しようとする呼び出されるこれらのルーチンの頻度を減らすと、ルーチンを見てくださいまたはこれらのルーチンに費やした時間。

-   ネットワーク アダプター ドライバーが全体的なシステム パフォーマンスの低下の原因となる、過剰なシステム リソースを使用しないように、DPC に費やされた時間を削減します。

-   ドライバーの場合は、最終リリース バージョンにコードのデバッグをコンパイルされないことを確認します。これは、余分なコードを実行して回避できます。

## <a name="partitioning-data-and-code-to-minimize-sharing-across-processors"></a>データとを最小限に抑えるプロセッサ間で共有コードをパーティション分割


プロセッサ間で共有データとコードを最小限に抑えるには、パーティション分割が必要です。 パーティション分割して、システム バスの使用率を減らすことが、プロセッサのキャッシュの有効性が向上します。 共有を最小限に抑えるには、ドライバーの作成者は、次の点を考慮する必要があります。

-   」の説明に従って、として逆シリアル化されたミニポート ドライバーを実装[NDIS ミニポート ドライバーの逆シリアル化](deserialized-ndis-miniport-drivers.md)します。

-   プロセッサごとのデータ構造を使用すると、グローバルと共有データへのアクセスを削減できます。 これにより、コード パスの長さを短縮されパフォーマンスが向上する、同期なしの統計カウンターを保持することができます。 重要な統計情報のクエリ時に一緒に追加するプロセッサごとのカウンターがあります。 グローバル カウンタが必要な場合は、スピン ロックではなくインタロックされた操作を使用して、カウンターを操作します。 適切に表示を使用してロック メカニズムの下をスピン ロックを使わないようにする方法についてはします。

    これを容易に[ **KeGetCurrentProcessorNumberEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552076)現在のプロセッサを決定するために使用できます。 プロセッサごとのデータ構造体を割り当てるときに、プロセッサの数を決定する[ **KeQueryGroupAffinity** ](https://msdn.microsoft.com/library/windows/hardware/ff553007)ことができます。

    関係マスクで設定されたビット数の合計は、システムでアクティブなプロセッサの数を示します。 ドライバーでは、プロセッサ可能性がありますしない連続番号が付けられます、将来のリリースのオペレーティング システムのため、マスク内のすべての設定済みビットが連続することは想定しないでください。 SMP マシンのプロセッサ数は、0 から始まる値です。

    使用することができます、ドライバーが、プロセッサごとのデータを保持する場合、 [ **KeQueryGroupAffinity** ](https://msdn.microsoft.com/library/windows/hardware/ff553007)キャッシュ ラインの競合を減らす関数。

## <a name="avoiding-false-sharing"></a>偽共有の回避


偽共有は、プロセッサは互いに独立して共有の変数を要求するときに発生します。 ただし、変数が同じキャッシュ ライン上にあるためはプロセッサ間で共有されます。 このような状況では、キャッシュ ラインがすべてのアクセスには、キャッシュのフラッシュで増加の原因で、変数のいずれかのプロセッサ間で前後へ移動し、再度読み込みます。 これにより、システム バスの使用率が向上し、全体的なシステム パフォーマンスが低下します。

偽共有を避けるためを使用してキャッシュ ラインの境界にスピン ロック、バッファー キュー ヘッダー、シングル リンク リスト) などの重要なデータ構造体を整列します。 [ **NdisGetSharedDataAlignment**](https://msdn.microsoft.com/library/windows/hardware/ff562671)します。

## <a name="using-locking-mechanisms-properly"></a>ロック メカニズムを正しく使用します。


スピン ロックが正しく使用されていなければパフォーマンスが低下することができます。 ドライバーは、可能な場合は、インタロックされた操作を使用して、スピン ロックの使用を最小限に抑える必要があります。 ただし、場合によっては、スピン ロックあります最適何らの目的で。 たとえば、ドライバーは、ドライバーに示されているいないパケットの数の参照カウントを処理中に、スピン ロックを取得する場合は、インタロックされた操作を使用する必要はありません。 詳細については、次を参照してください。[同期とネットワーク ドライバーに通知](synchronization-and-notification-in-network-drivers.md)します。

ロック メカニズムを効果的に使用するためのヒントを次に示します。

-   リソース プールを管理するためには、次のよう NDIS シングル リンク リストの関数を使用します。

    [**NdisInitializeSListHead**](https://msdn.microsoft.com/library/windows/hardware/ff562739)

    [**NdisInterlockedPushEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff562764)

    [**NdisInterlockedPopEntrySList**](https://msdn.microsoft.com/library/windows/hardware/ff562760)

    [**NdisQueryDepthSList**](https://msdn.microsoft.com/library/windows/hardware/ff563753)

-   スピン ロックを使用する必要がある場合は、コードではなく、データの保護のみを使用します。 一般的なパスで使用されるすべてのデータを保護するのに 1 つのロックを使用しないでください。 たとえば、送信パスでは、そのデータをロックする必要がある、受信パスは影響されないように、2 つのデータ構造に、送信と受信パスで使用されるデータを区切ります。

-   スピン ロックを使用している場合に、パスが既に DPC レベルを使用して、 [ **NdisDprAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff561749)と[ **NdisDprReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff561753)余分なコードを取得すると、ロックの解放を回避する関数。

-   スピン ロックの数を最小限に抑えるを取得し、リリースでは、これらの NDIS RWLock 関数を使用します。

    [**NdisAllocateRWLock**](https://msdn.microsoft.com/library/windows/hardware/ff561615)

    [**NdisAcquireRWLockRead**](https://msdn.microsoft.com/library/windows/hardware/ff560697)

    [**NdisAcquireRWLockWrite**](https://msdn.microsoft.com/library/windows/hardware/ff560698)

    [**NdisReleaseRWLock**](https://msdn.microsoft.com/library/windows/hardware/ff564523)

## <a name="using-64-bit-dma"></a>64 ビットの DMA を使用してください。


64 ビット DMA 場合、ネットワーク アダプターは、64 ビットの DMA をサポートする、4 GB の範囲より上のアドレスの余分なコピーを回避するために、手順を実行する必要があります。 ドライバーを呼び出すと[ **NdisMRegisterScatterGatherDma**](https://msdn.microsoft.com/library/windows/hardware/ff563659)、 **NDIS\_SG\_DMA\_64\_ビット\_アドレス**フラグを設定する必要があります、*フラグ*パラメーター。

## <a name="ensuring-proper-buffer-alignment"></a>適切なバッファーのアライメントを確保します。


キャッシュ ラインの境界上のバッファーの配置では、別に 1 つのバッファーからデータをコピーするときにパフォーマンスが向上します。 ほとんどのネットワーク アダプターの受信バッファーが割り当てられる最初がヘッダーの空き容量が消費される整列されていないアプリケーションのバッファーにコピーする必要が最終的にユーザー データが正しく調整します。 TCP データ (最も一般的なシナリオ) の場合は、shift キーを押し、TCP、IP およびイーサネット ヘッダーにより結果 0x36 バイトのシフトします。 この問題を解決するには、ドライバーは少し大きめのバッファーを割り当てるし、0 xa のバイト オフセット位置でのパケット データを挿入お勧めします。 、0x36 バイトのヘッダーでは、バッファーがシフトされ、後にユーザー データが正しく配置されるようになります。 キャッシュ ラインの境界の詳細については、「解説」を参照してください。 [ **NdisMAllocateSharedMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562782)します。

## <a name="using-scatter-gather-dma"></a>スキャッター/ギャザー DMA を使用します。


[NDIS スキャッター/ギャザー DMA](ndis-scatter-gather-dma.md)と物理メモリの不連続な範囲からデータの転送に対応ハードウェアを提供します。 スキャッター/ギャザー DMA を使用して、 [**散布図\_収集\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff563664) 、構造体の配列を含む**散布図\_収集\_要素**構造と、配列内の要素の数。 この構造体は、ドライバーの送信の関数に渡されるパケット記述子から取得されます。 配列の各要素は、長さと物理的に連続するスキャッター/ギャザー リージョンの物理アドレスの開始を提供します。 ドライバーは、データを転送するため、長さとアドレス情報を使用します。

DMA 操作のスキャッター/ギャザー ルーチンを使用すると、静的にマップを登録する場合に発生するをこれらのリソースをロックしないことによってリソースが使用されたシステムの使用率が向上します。 詳細については、次を参照してください。 [NDIS スキャッター/ギャザー DMA](ndis-scatter-gather-dma.md)します。

ネットワーク アダプターは、TCP セグメント化オフロード (Large Send Offload) をサポートしているかどうかは、ドライバーに TCP/IP から取得できる最大バッファー サイズを渡す必要があります、 *MaximumPhysicalMapping*内でパラメーター [ **NdisMRegisterScatterGatherDma** ](https://msdn.microsoft.com/library/windows/hardware/ff563659)関数。 ドライバーが十分なマップのレジスタをスキャッター/ギャザーのリストを作成し、可能なバッファーの割り当てを削除するようにし、コピーします。 詳しくは、次のトピックをご覧ください。

- [タスクのオフロード機能を判断します。](determining-task-offload-capabilities.md)
- [大きな TCP パケットのセグメント化をオフロード](offloading-the-segmentation-of-large-tcp-packets.md)

## <a name="supporting-receive-side-throttle"></a>受信側のスロットルのサポート


マルチ メディア アプリケーション、NDIS 6.20 が動作し、以降のドライバーでメディアの再生中に中断を最小限に抑える必要があります処理の受信側スロットル (RST) 受信サポート割り込みです。 詳細については、以下をご覧ください。

[受信側のスロットルを NDIS 6.20 が動作で](receive-side-throttle-in-ndis-6-20.md)「送信し、受信コード パス」で[NDIS 6.20 が動作するためのミニポート ドライバーを移植するために必要な変更の概要](summary-of-changes-required-to-port-a-miniport-driver-to-ndis-6-20.md)
 

 





