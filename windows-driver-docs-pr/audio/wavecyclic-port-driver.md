---
title: WaveCyclic ポート ドライバー
description: WaveCyclic ポート ドライバー
ms.assetid: c5572ae3-0d91-43a6-a49c-c6c005263f5b
keywords:
- WaveCyclic port driver WDK audio
- PortCls WDK オーディオ、ポートドライバー
- オーディオミニポートドライバー WDK、ポートドライバー
- ミニポートドライバー WDK オーディオ、ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53c27896c4b149d04a2f3be702b656e3d48c6206
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833999"
---
# <a name="wavecyclic-port-driver"></a>WaveCyclic ポート ドライバー


## <span id="wavecyclic_port_driver"></span><span id="WAVECYCLIC_PORT_DRIVER"></span>


**重要**  WaveCyclic の使用は推奨されなくなりました。代わりに WaverRT を使用してください。

 

WaveCyclic port ドライバーは、循環バッファー内のオーディオデータを処理する DMA ベースのオーディオデバイスによる wave ストリームの再生または記録を管理します。 このデバイスは、オーディオアダプターのハードウェア機能です。 通常、アダプターは、マザーボード上の統合チップセットの一部であるか、またはマザーボード上の PCI または ISA スロットに接続するオーディオカードに取り付けられています。 アダプタードライバーは、対応する[WaveCyclic ミニポートドライバー](wavecyclic-miniport-driver.md)のドライバーオブジェクトを提供します。このオブジェクトは、WaveCyclic port driver オブジェクトにバインドして、wave ストリームをキャプチャまたはレンダリングできる[wave フィルター](wave-filters.md)を形成します。

WaveCyclic port ドライバーは、 [IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)インターフェイスをミニポートドライバーに公開します。 IPortWaveCyclic は、基本インターフェイス[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)のメソッドを継承します。 IPortWaveCyclic には、次の追加のメソッドが用意されています。

[**IPortWaveCyclic::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

組み込み DMA コントローラーを備えたオーディオデバイス用の新しいマスター DMA チャネルオブジェクトを作成します。

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

組み込みの DMA コントローラーを使用せずに、オーディオデバイス用の新しい下位 DMA チャネルオブジェクトを作成します。

[**IPortWaveCyclic:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-notify)

DMA コントローラーがオーディオストリーム内の新しい位置に進んでいることをポートドライバーに通知します。

WaveCyclic port オブジェクトとミニポートドライバーオブジェクトは、それぞれの[IPortWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic)インターフェイスと[IMiniportWaveCyclic](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic)インターフェイスを介して相互に通信します。 さらに、ポートドライバーは、 [IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)インターフェイスを介してミニポートドライバーのストリームオブジェクトと通信します。

 

 




