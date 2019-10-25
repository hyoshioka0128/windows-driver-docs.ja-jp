---
title: WavePci ミニポート ドライバーにおける信頼性の問題
description: WavePci ミニポート ドライバーにおける信頼性の問題
ms.assetid: 329f28a8-5e99-4c25-8a88-1e634f7eeec8
keywords:
- WavePci の信頼性に関する問題 (WDK オーディオ)
- スピンロック WDK オーディオ
- Irp の取り消し
- デッドロック WDK オーディオ
- 割り込みサービスルーチン WDK オーディオ
- Isr WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd2b0f8b12ddc4a70b1cedc789155920ad0ff55c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832435"
---
# <a name="reliability-issues-for-a-wavepci-miniport-driver"></a>WavePci ミニポート ドライバーにおける信頼性の問題


## <span id="reliability_issues_for_a_wavepci_miniport_driver"></span><span id="RELIABILITY_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


WavePci ミニポートドライバーは、ポートドライバーから受信したマッピングを追跡する必要があります。 WavePci ミニポートドライバーは、ドライバースレッド間で共有されるデータ構造内のマッピングの一覧を保持します。 また、ドライバースレッドは、新しいマッピングをハードウェアキューに追加し、完了したマッピングをキューから削除するために、DMA チャネルへのアクセスも共有する必要があります。 データの破損を防ぐために、ミニポートドライバーは、スピンロックを使用して、共有データ構造および周辺機器へのアクセスをシリアル化します。 スピンロックは、共有データとハードウェアキューが2つ以上のドライバースレッドによる同時アクセスから保護されます。

マッピングを管理するドライバーの部分を開発する場合、ベンダーは次の点に特に注意を払う必要があります。

### <a name="span-idspin_locksspanspan-idspin_locksspanspan-idspin_locksspanspin-locks"></a><span id="Spin_Locks"></span><span id="spin_locks"></span><span id="SPIN_LOCKS"></span>スピンロック

デッドロックの可能性を回避するには、Portcls を呼び出してマッピングを取得または解放するときに、ミニポートドライバーが独自のスピンロックを保持しないようにする必要があります。 Microsoft Windows Driver Kit (WDK) の Ac97 サンプルドライバーは、この原則を示しています。 [**Iportwavepcistream:: GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)または[**Iportwavepcistream:: ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping)を呼び出す前に、サンプルドライバーは[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)を呼び出して、スピンロックを解放します。 **Getmapping**または**ReleaseMapping**呼び出しが返された後、ドライバーは[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)を呼び出して、スピンロックを再度取得します。 リリースへの呼び出しとスピンロックの取得の間で、ドライバースレッドは、マッピングの一覧に排他的にアクセスできることを前提としてはなりません。 この保護されていない間隔中に共有データにアクセスすることは危険です。 スピンロックの解放と取得の間隔が小さい場合、2つのドライバースレッド間の競合状態によってデータが破損する可能性も小さくなります。 これは、結果として発生するエラーが断続的で、トレースが困難であることを意味します。 スピンロックを解放して取得した後、適切に記述されたドライバーでは、共有データ構造のコンテンツにアクセスするために以前使用した一時ポインターまたはインデックスが無効になっていることを前提としています。

### <a name="span-idirp_cancellationspanspan-idirp_cancellationspanspan-idirp_cancellationspanirp-cancellation"></a><span id="IRP_Cancellation"></span><span id="irp_cancellation"></span><span id="IRP_CANCELLATION"></span>IRP のキャンセル

再生ストリームまたはキャプチャストリームの処理中にいつでも、IRP をキャンセルすると、オペレーティングシステムによって、ミニポートドライバーによって取得された1つ以上のマッピングが失効する可能性があります。 このエラーが発生すると、ポートドライバーは[**IMiniportWavePciStream:: RevokeMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-revokemappings)メソッドを呼び出してミニポートドライバーに通知します。 失効したマッピングへのデータの再生またはデータのキャプチャを避けるために、ミニポートドライバーは、そのソフトウェアの一覧と DMA コントローラーのハードウェアキューの両方からマッピングを削除する必要があります。 ソフトウェアの一覧とハードウェアキューはドライバーのスレッド間で共有されるため、これらの操作を確実に実行するには注意が必要です。

たとえば、取り消し対象の一連のマッピングには、直前にリリースされたか、直前にリリースされたマッピングが含まれている場合があります。 この場合、2つのドライバースレッドが DMA キューから同じマッピングを同時に削除しようとすることがあります。 ドライバーが同時アクセスを防止できない場合は、キューを管理するレジスタまたはメモリ構造のデータが破損している可能性があります。

実際のコード例については、Windows Driver Kit (WDK) の Ac97 サンプルドライバーを参照してください。

 

 




