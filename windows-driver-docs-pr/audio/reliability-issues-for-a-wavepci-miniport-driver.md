---
title: WavePci ミニポート ドライバーにおける信頼性の問題
description: WavePci ミニポート ドライバーにおける信頼性の問題
ms.assetid: 329f28a8-5e99-4c25-8a88-1e634f7eeec8
keywords:
- WavePci 信頼性の問題の WDK オーディオ
- スピン ロック WDK オーディオ
- Irp のキャンセル
- デッドロック WDK オーディオ
- 割り込みサービス ルーチン WDK オーディオ
- Isr WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de6e1891de1f7443b1e1a0566904c975a61617cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362505"
---
# <a name="reliability-issues-for-a-wavepci-miniport-driver"></a>WavePci ミニポート ドライバーにおける信頼性の問題


## <span id="reliability_issues_for_a_wavepci_miniport_driver"></span><span id="RELIABILITY_ISSUES_FOR_A_WAVEPCI_MINIPORT_DRIVER"></span>


WavePci ミニポート ドライバーする必要がありますの追跡、ポート ドライバーから受信したマッピング。 WavePci ミニポート ドライバーは、ドライバーのスレッド間で共有されるデータ構造内のマッピングのリストを保持しています。 ドライバーのスレッドでは、ハードウェア キューに新しいマッピングを追加して、キューから完成したマッピングを削除するには、DMA チャネルへのアクセスは共有もする必要があります。 ミニポート ドライバーはデータの破損を防ぐためには、スピン ロックを使用して、共有データ構造と周辺機器へのアクセスをシリアル化します。 スピン ロックは共有データおよびハードウェア キューを 2 つ以上のドライバーのスレッドによって同時アクセスから保護します。

マッピングを管理するドライバーの部分を開発するときに、ベンダーは特に、次の点に注意を払う必要があります。

### <a name="span-idspinlocksspanspan-idspinlocksspanspan-idspinlocksspanspin-locks"></a><span id="Spin_Locks"></span><span id="spin_locks"></span><span id="SPIN_LOCKS"></span>スピン ロック

取得するか、マッピングをリリースする Portcls.sys を呼び出すときに、ミニポート ドライバー潜在的なデッドロックを回避するには、スピン ロックは保持でする必要がありますしません。 Microsoft Windows Driver Kit (WDK) でのドライバーの Ac97 サンプルは、この原則を示しています。 いずれかを呼び出す前に[ **IPortWavePciStream::GetMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping)または[ **IPortWavePciStream::ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-releasemapping)ドライバーのサンプル呼び出し[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)スピン ロックを解除します。 後に、 **GetMapping**または**ReleaseMapping**戻り値は、ドライバーの呼び出しを呼び出す[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)をもう一度、スピン ロックを取得します。 リリースし、スピン ロックの取得の呼び出しを間 driver スレッドする必要がありますわけではマッピングの一覧への排他アクセスがあります。 この保護されていない間隔中に共有データにアクセスするは危険です。 解放、スピン ロックを取得するまでの間隔が小さい場合、ドライバーの 2 つのスレッド間の競合状態が破損しているデータの可能性が小さい。 これは、ため、結果として得られるエラーは断続的にトレースするために困難です。 解放、スピン ロックを取得すると、適切に記述されたドライバーは、一時的なポインターや共有データ構造体の内容にアクセスを使用していたインデックスが不要になった有効であると想定されます。

### <a name="span-idirpcancellationspanspan-idirpcancellationspanspan-idirpcancellationspanirp-cancellation"></a><span id="IRP_Cancellation"></span><span id="irp_cancellation"></span><span id="IRP_CANCELLATION"></span>IRP のキャンセル

再生またはキャプチャ ストリームの処理中にいつでも IRP のキャンセルにオペレーティング システムをミニポート ドライバーで取得した 1 つまたは複数のマッピングを取り消すことがあります。 この場合、ポートのドライバーを呼び出す、 [ **IMiniportWavePciStream::RevokeMappings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-revokemappings)ミニポート ドライバーに通知するメソッド。 失効したマッピングからデータを再生中またはデータのキャプチャのいずれかを回避するために、ミニポート ドライバーをそのソフトウェアの一覧および DMA コント ローラーのハードウェア キューの両方からのマッピングを削除する必要があります。 ソフトウェアの一覧とハードウェアのキューは、ドライバーのスレッド間で共有される、ために、これらの操作を確実に実行するいくつか注意が必要です。

たとえば、一連マッピングを無効にするにはには、マッピングされただけかを解放するが含まれます。 この場合、ドライバーの 2 つのスレッドは可能性があります、DMA キューから同じマッピングを削除する同時に試行しました。 ドライバーは、同時アクセスを防ぐために失敗した場合、結果のレジスタまたはキューを管理するメモリ構造内のデータの破損を使用できます。

実際のコード例は、Windows Driver Kit (WDK) でのドライバーの Ac97 サンプルを参照してください。

 

 




