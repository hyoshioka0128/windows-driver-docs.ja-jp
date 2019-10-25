---
title: WavePci ミニポート ドライバー
description: WavePci ミニポート ドライバー
ms.assetid: 8a166087-d158-4d49-a917-2a5a78b43cb4
keywords:
- オーディオミニポートドライバー WDK、WavePci
- ミニポートドライバー WDK audio、WavePci
- WavePci ミニポートドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac464be6fea3c7245f50be4053aa45916ebebfd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829963"
---
# <a name="wavepci-miniport-driver"></a>WavePci ミニポート ドライバー


## <span id="wavepci_miniport_driver"></span><span id="WAVEPCI_MINIPORT_DRIVER"></span>


**重要**  WavePci の使用は推奨されなくなりました。代わりに WaverRT を使用してください。

 

WavePci ミニポートドライバーは、物理メモリ内の任意の場所との間でオーディオデータを転送できるスキャッター/ギャザー DMA ハードウェアを備えた、wave レンダリングまたは wave キャプチャデバイスのハードウェアに依存する機能を管理します。 スキャッター/ギャザー転送を実行できないか、または物理メモリ内の制限された領域にのみアクセスできる wave デバイスでは、代わりに[WaveCyclic ミニポートドライバー](wavecyclic-miniport-driver.md)を使用する必要があります。

WavePci ミニポートドライバーは、次の2つのインターフェイスを実装する必要があります。

-   **ミニポートインターフェイスは**、ミニポートドライバーの初期化、チャネル列挙、およびストリーム作成を実行します。

-   **ストリームインターフェイスは**、wave ストリームを管理し、ほとんどのミニポートドライバーの機能を公開します。

ミニポートインターフェイス[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)は、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)インターフェイスのメソッドを継承します。 IMiniportWavePci には、次の追加のメソッドが用意されています。

[**IMiniportWavePci:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

ミニポートオブジェクトを初期化します。

[**IMiniportWavePci:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)

新しいストリームオブジェクトを作成します。

[**IMiniportWavePci:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-service)

サービスの要求をミニポートドライバーに通知します。

ストリームインターフェイス[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)は、 [**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)インターフェイスからメソッドを継承します。 IMiniportWavePciStream には、次の追加のメソッドが用意されています。

[**IMiniportWavePciStream:: GetAllocatorFraming**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing)

Wave ストリームに対するミニポートドライバーの推奨されるアロケーターフレームパラメーターを取得します。

[**IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)

Wave ストリーム内のデバイスの現在位置を取得します。

[**IMiniportWavePciStream:: MappingAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-mappingavailable)

ポートドライバーから新しいマッピングを使用できることを示します。

[**IMiniportWavePciStream:: NormalizePhysicalPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-normalizephysicalposition)

物理バッファーの位置の値を時間ベースの値に変換します。

[**IMiniportWavePciStream::RevokeMappings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-revokemappings)

以前に発行されたマッピングを取り消します。

[**IMiniportWavePciStream:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)

サービスの要求のストリームオブジェクトに通知します。

[**IMiniportWavePciStream:: SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setformat)

Wave ストリームのデータ形式を設定します。

[**IMiniportWavePciStream:: SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setstate)

Wave ストリームの状態を設定します。
 

 




