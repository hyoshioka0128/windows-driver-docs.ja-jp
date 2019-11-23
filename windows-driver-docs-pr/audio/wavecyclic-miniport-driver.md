---
title: WaveCyclic ミニポート ドライバー
description: WaveCyclic ミニポート ドライバー
ms.assetid: 8a4811e9-e52b-4183-8d11-482883500f82
keywords:
- オーディオミニポートドライバー WDK、WaveCyclic
- ミニポートドライバー WDK audio、WaveCyclic
- WaveCyclic ミニポートドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77d080e104e9e4de453be7a5c11aed567383b1e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832299"
---
# <a name="wavecyclic-miniport-driver"></a>WaveCyclic ミニポート ドライバー


## <span id="wavecyclic_miniport_driver"></span><span id="WAVECYCLIC_MINIPORT_DRIVER"></span>


**重要**  WavePci の使用は推奨されなくなりました。代わりに WaverRT を使用してください。

 

WaveCyclic ミニポートドライバーは、オーディオデータ用の循環バッファーを使用する、wave レンダリングデバイスまたは wave キャプチャデバイスのハードウェアに依存する機能を管理します。 循環バッファーは、通常、連続する物理メモリの1つのブロックであり、ドライバーが選択したメモリ領域に配置できます。 次の制限事項を持つデバイスは、 [WavePci ミニポートドライバー](wavepci-miniport-driver.md)ではなく、WaveCyclic ミニポートドライバーを提供する必要があります。

-   デバイスに DMA ハードウェアがありません。

-   デバイスの DMA ハードウェアは、連続する物理メモリの1つのブロックを占有するバッファー内のデータにのみアクセスできます。

-   デバイスの DMA ハードウェアは、物理メモリのすべてのリージョンのデータにアクセスできません。

WaveCyclic ミニポートドライバーは、次の2つのインターフェイスを実装する必要があります。

-   **ミニポートインターフェイスでは、** ミニポートドライバーの初期化とストリームの作成がサポートされています。

-   **ストリームインターフェイスは**、wave ストリームを管理し、ほとんどのミニポートドライバーの機能を公開します。

ミニポートインターフェイス[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)は、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)インターフェイスのメソッドを継承します。 IMiniportWaveCyclic には、次の追加のメソッドが用意されています。

[**IMiniportWaveCyclic::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-init)

ミニポートオブジェクトを初期化します。

[**IMiniportWaveCyclic:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)

新しいストリームオブジェクトを作成します。

ストリームインターフェイス[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)は、 [**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイスのメソッドを継承します。 IMiniportWaveCyclicStream には、次の追加のメソッドが用意されています。

[**IMiniportWaveCyclicStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition)

Wave ストリーム内のデバイスの現在位置を取得します。

[**IMiniportWaveCyclicStream:: NormalizePhysicalPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-normalizephysicalposition)

物理バッファーの位置の値を時間ベースの値に変換します。

[**IMiniportWaveCyclicStream:: SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-setformat)

Wave ストリームのデータ形式を設定します。

[**IMiniportWaveCyclicStream::SetNotificationFreq**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-setnotificationfreq)

通知割り込みが発生する頻度を設定します。

[**IMiniportWaveCyclicStream:: SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-setstate)

Wave ストリームの状態を設定します。

[**IMiniportWaveCyclicStream:: 無音**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-silence)

無音状態をバッファーにコピーします。
 

 




