---
title: WavePci ポート ドライバー
description: WavePci ポート ドライバー
ms.assetid: 3b4a89d0-f07a-40e1-8c67-62d9cfd96ddd
keywords:
- WavePci port driver WDK audio
- PortCls WDK オーディオ、ポートドライバー
- オーディオミニポートドライバー WDK、ポートドライバー
- ミニポートドライバー WDK オーディオ、ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1056633247abc631855482c409d6ec86cdf5cda3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829931"
---
# <a name="wavepci-port-driver"></a>WavePci ポート ドライバー


## <span id="wavepci_port_driver"></span><span id="WAVEPCI_PORT_DRIVER"></span>


**重要**  WavePci の使用は推奨されなくなりました。代わりに WaverRT を使用してください。

 

WavePci port ドライバーは、物理メモリ内の任意の場所との間でのスキャッター/ギャザー DMA 転送を実行できるオーディオデバイスによる wave ストリームの再生または記録を管理します。 スキャッター/gather DMA を使用すると、デバイスは一連のマッピングで構成されるバッファー内のオーディオデータを処理できます。 各マッピングは物理的に連続したメモリのブロックですが、連続するマッピングは必ずしも連続しているとは限りません。 WavePci と互換性のあるデバイスは、オーディオアダプターのハードウェア機能です。 通常、アダプターは、マザーボード上の統合チップセットの一部であるか、またはマザーボード上の PCI スロットに接続するオーディオカードに取り付けられています。 アダプタードライバーは、対応する[WavePci ミニポートドライバー](wavepci-miniport-driver.md)を提供します。これは、WavePci port driver オブジェクトにバインドして、wave ストリームをキャプチャまたはレンダリングできる[wave フィルター](wave-filters.md)を形成します。

WavePci port ドライバーは、 [IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))インターフェイスをミニポートドライバーに公開します。 IPortWavePci は、基本インターフェイス[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)のメソッドを継承します。 さらに、IPortWavePci には次のメソッドが用意されています。

[**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-newmasterdmachannel)

新しいマスター DMA チャネルオブジェクトを作成します。
[**IPortWavePci:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)

DMA コントローラーがオーディオストリーム内の新しい位置に進んでいることをポートドライバーに通知します。
また、WavePci port ドライバーは、各ミニポートドライバーのストリームオブジェクトへの[Iportwavepcistream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream)インターフェイスも公開します。 IPortWavePciStream は、基本インターフェイス[**IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)のメソッドを継承します。 IPortWavePciStream には、次の追加のメソッドが用意されています。

[**IPortWavePciStream:: GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)

ポートドライバーから次のマッピングを取得します。
[**IPortWavePciStream:: ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping)

以前に**getmapping**呼び出しによって取得されたマッピングを解放します。
[**IPortWavePciStream:: TerminatePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-terminatepacket)

キャプチャデータが部分的に入力されている場合でも、i/o パケットを終了します。
I/o パケットは、特定のマッピングの IRP に関連付けられているすべてのマッピングで構成されるオーディオバッファーの一部です。

WavePci port オブジェクトとミニポートオブジェクトは、それぞれの[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))インターフェイスと[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci)インターフェイスを介して相互に通信します。 さらに、WavePci port オブジェクトとミニポートストリームオブジェクトは、それぞれの[Iportwavepcistream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream)および[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)インターフェイスを介して相互に通信します。

 

 




