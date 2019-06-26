---
title: WaveCyclic ポート ドライバー
description: WaveCyclic ポート ドライバー
ms.assetid: c5572ae3-0d91-43a6-a49c-c6c005263f5b
keywords:
- WaveCyclic ポート ドライバー WDK オーディオ
- PortCls WDK のオーディオ、ポートのドライバー
- オーディオのミニポート ドライバー WDK、ポート ドライバー
- ミニポート ドライバー WDK のオーディオ、ポートのドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c10aac267a6ecf3d4646fedb5f85375d7ce5d431
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364793"
---
# <a name="wavecyclic-port-driver"></a>WaveCyclic ポート ドライバー


## <span id="wavecyclic_port_driver"></span><span id="WAVECYCLIC_PORT_DRIVER"></span>


**重要な**  WaveCyclic の使用は推奨されなく、WaverRT を代わりに使用します。

 

WaveCyclic ポート ドライバーは、DMA ベースのオーディオ デバイスで、循環バッファー内のオーディオ データを処理して、再生や wave ストリームの記録を管理します。 このデバイスは、オーディオのアダプターのハードウェア機能です。 通常、アダプターは、統合されたチップセット、マザーボード上の一部であるまたはマザーボードの PCI または ISA スロットに差し込まれるオーディオのカードにマウントされています。 アダプターのドライバーは、対応する[WaveCyclic ミニポート ドライバー](wavecyclic-miniport-driver.md)フォームに WaveCyclic ポート ドライバー オブジェクトにバインドするドライバー オブジェクト、 [wave フィルター](wave-filters.md)キャプチャまたは wave ストリームをレンダリングすることができます。

WaveCyclic ポート ドライバーを公開、 [IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic)ミニポート ドライバーへのインターフェイス。 IPortWaveCyclic 基底インターフェイスのメソッドを継承する[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)します。 IPortWaveCyclic では、次の追加のメソッドを提供します。

[**IPortWaveCyclic::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

組み込みの DMA コント ローラーで、オーディオ デバイスの新しいマスター DMA チャネル オブジェクトを作成します。

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

組み込みの DMA コント ローラーなし、オーディオ デバイスの新しい下位 DMA チャネル オブジェクトを作成します。

[**IPortWaveCyclic::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavecyclic-notify)

DMA コント ローラーにオーディオ ストリーム内の新しい位置に高度なポート ドライバーに通知します。

WaveCyclic ポートおよびミニポート ドライバー オブジェクトは、それぞれを互い通信[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavecyclic)と[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclic)インターフェイス。 さらに、ポート ドライバーと通信を介して、ミニポート ドライバーのストリーム オブジェクト、 [IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclicstream)インターフェイス。

 

 




