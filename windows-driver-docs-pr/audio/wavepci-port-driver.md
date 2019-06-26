---
title: WavePci ポート ドライバー
description: WavePci ポート ドライバー
ms.assetid: 3b4a89d0-f07a-40e1-8c67-62d9cfd96ddd
keywords:
- WavePci ポート ドライバー WDK オーディオ
- PortCls WDK のオーディオ、ポートのドライバー
- オーディオのミニポート ドライバー WDK、ポート ドライバー
- ミニポート ドライバー WDK のオーディオ、ポートのドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25dd17f1cfa3cde254a6908f9c1a2fe8bc5e6cb6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354107"
---
# <a name="wavepci-port-driver"></a>WavePci ポート ドライバー


## <span id="wavepci_port_driver"></span><span id="WAVEPCI_PORT_DRIVER"></span>


**重要な**  WavePci の使用は推奨されなく、WaverRT を代わりに使用します。

 

ポート ドライバー、オーディオ デバイスを実行できる再生または wave ストリームの記録を管理する WavePci スキャッター/ギャザー DMA 転送するか、物理メモリ内の任意の場所からします。 スキャッター/ギャザー DMA、デバイスは、一連のマッピングで構成されるバッファー内のオーディオ データを処理できます。 各マッピングが物理的に連続するメモリのブロックが連続するマッピングが相互に必ずしも連続していません。 WavePci と互換性のあるデバイスは、オーディオのアダプターのハードウェア機能です。 通常、アダプターは、統合されたチップセット、マザーボード上の一部であるまたはマザーボードの PCI スロットに差し込まれるオーディオのカードにマウントされています。 対応するアダプターのドライバーを提供します[WavePci ミニポート ドライバー](wavepci-miniport-driver.md)フォームに WavePci ポート ドライバー オブジェクトをバインドする、 [wave フィルター](wave-filters.md)キャプチャまたは wave ストリームをレンダリングすることができます。

WavePci ポート ドライバーを公開、 [IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))ミニポート ドライバーへのインターフェイス。 IPortWavePci 基底インターフェイスのメソッドを継承する[IPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iport)します。 さらに、IPortWavePci は、次のメソッドを提供します。

[**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-newmasterdmachannel)

新しいマスター DMA チャネル オブジェクトを作成します。
[**IPortWavePci::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)

DMA コント ローラーにオーディオ ストリーム内の新しい位置に高度なポート ドライバーに通知します。
WavePci ポート ドライバーも公開、 [IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavepcistream)のミニポート ドライバーのストリーム オブジェクトへのインターフェイス。 IPortWavePciStream 基底インターフェイスのメソッドを継承する[ **IUnknown**](https://docs.microsoft.com/windows/desktop/api/unknwn/nn-unknwn-iunknown)します。 IPortWavePciStream では、次の追加のメソッドを提供します。

[**IPortWavePciStream::GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping)

ポート ドライバーから次のマッピングを取得します。
[**IPortWavePciStream::ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-releasemapping)

によって以前に取得されているマッピングの解放、 **GetMapping**呼び出します。
[**IPortWavePciStream::TerminatePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-terminatepacket)

部分的にのみキャプチャ データでいっぱいになった場合でも、I/O のパケットを終了します。
I/O のパケットは、特定の IRP マッピングに関連付けられているすべてのマッピングで構成されるバッファーの一部です。

WavePci ポートおよびミニポートのオブジェクトが、それぞれを互い通信[IPortWavePci](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536905(v=vs.85))と[IMiniportWavePci](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepci)インターフェイス。 さらに、WavePci ポートおよびミニポートのストリーム オブジェクト相互通信をそれぞれ[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavepcistream)と[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)インターフェイス。

 

 




