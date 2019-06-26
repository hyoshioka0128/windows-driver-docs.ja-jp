---
title: WaveCyclic ミニポート ドライバー
description: WaveCyclic ミニポート ドライバー
ms.assetid: 8a4811e9-e52b-4183-8d11-482883500f82
keywords:
- オーディオのミニポート ドライバー WDK、WaveCyclic
- ミニポート ドライバー WDK オーディオ、WaveCyclic
- WaveCyclic ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43000886805d646dcfebf29ef074525f74c50ee7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354110"
---
# <a name="wavecyclic-miniport-driver"></a>WaveCyclic ミニポート ドライバー


## <span id="wavecyclic_miniport_driver"></span><span id="WAVECYCLIC_MINIPORT_DRIVER"></span>


**重要な**  WavePci の使用は推奨されなく、WaverRT を代わりに使用します。

 

WaveCyclic ミニポート ドライバーでは、wave レンダリングまたはオーディオ データの循環バッファーを使用して wave キャプチャ デバイスのハードウェアに依存する関数を管理します。 循環バッファーは、連続した物理メモリの 1 つのブロックは、通常とドライバーの選択のメモリの領域にあることができます。 次の制限事項のいずれかを使用したデバイスが WaveCyclic ミニポート ドライバーを提供する必要がありますではなく[WavePci ミニポート ドライバー](wavepci-miniport-driver.md):

-   デバイスでは、DMA ハードウェアがありません。

-   デバイスの DMA ハードウェアは、連続した物理メモリの 1 つのブロックを占有するバッファーにのみデータにアクセスできます。

-   デバイスの DMA のハードウェアが物理メモリのすべてのリージョンでデータにアクセスできません。

WaveCyclic ミニポート ドライバーでは、2 つのインターフェイスを実装する必要があります。

-   **ミニポート インターフェイス**ミニポート ドライバーの初期化とストリームの作成をサポートします。

-   **ストリーム インターフェイス**wave ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic)でメソッドを継承、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)インターフェイス。 IMiniportWaveCyclic では、次の追加のメソッドを提供します。

[**IMiniportWaveCyclic::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-init)

ミニポート オブジェクトを初期化します。

[**IMiniportWaveCyclic::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)

新しいストリーム オブジェクトを作成します。

ストリーム インターフェイス、 [IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclicstream)でメソッドを継承、 [ **IUnknown** ](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイス。 IMiniportWaveCyclicStream では、次の追加のメソッドを提供します。

[**IMiniportWaveCyclicStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-getposition)

Wave ストリーム内のデバイスの現在位置を取得します。

[**IMiniportWaveCyclicStream::NormalizePhysicalPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-normalizephysicalposition)

時間ベースの値には、物理バッファー位置の値を変換します。

[**IMiniportWaveCyclicStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-setformat)

Wave ストリームのデータ形式を設定します。

[**IMiniportWaveCyclicStream::SetNotificationFreq**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-setnotificationfreq)

通知に割り込みが発生する頻度を設定します。

[**IMiniportWaveCyclicStream::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-setstate)

Wave ストリームの状態を設定します。

[**IMiniportWaveCyclicStream::Silence**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-silence)

バッファーにコピー アクティビティがない状態です。
 

 




