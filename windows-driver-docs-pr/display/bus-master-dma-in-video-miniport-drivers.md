---
title: ビデオ ミニポート ドライバーのバス マスター DMA
description: ビデオ ミニポート ドライバーのバス マスター DMA
ms.assetid: fe6c2e16-d222-4948-b1df-34ed8d57d9d8
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、バス マスター DMA
- バス マスター DMA WDK ビデオのミニポート
- DMA バス マスター WDK のビデオのミニポート
- 一般的なバッファー DMA WDK ビデオのミニポート
- 一般的なバッファー DMA WDK ビデオのミニポート, 概要
- パケットに基づく DMA WDK ビデオのミニポート
- パケットに基づく DMA WDK ビデオのミニポート, 概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40297b11d5225031b27f20f20ea64e3d56532154
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341594"
---
# <a name="bus-master-dma-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーのバス マスター DMA


## <span id="ddk_bus_master_dma_in_video_miniport_drivers_gg"></span><span id="DDK_BUS_MASTER_DMA_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


Windows XP 以降では、オペレーティング システムのグラフィックス インターフェイスは、PCI バス マスターのデバイス上の DMA をサポートします。 PCI バス マスターのデバイスのビデオのミニポート ドライバーでは、次の種類のビデオ ポート ドライバーによって提供されるヘルパー関数を使用して DMA サポートを実装できます。

-   **DMA のパケットに基づく**

    DMA のパケットに基づくデータが、要求元の場所とデバイス間で直接転送されます。 要求者の領域を連続することができない可能性があります、ために、パケットに基づく DMA は、スキャッター/ギャザーのハードウェア サポートとそれらのデバイスでより効率的です。 パケットに基づく DMA は、ユーザー空間と、デバイス間で大量の任意のデータを移動するための最適な選択肢です。

-   **一般的なバッファーの DMA**

    一般的なバッファーの DMA 間でバッファーを共有 (そのために共通する)、およびホストと DMA 操作を繰り返しについては、デバイスの両方で使用します。 一部のドライバーでは、グラフィックス エンジンに一連のコマンドなどのドライバー操作のデータをアップロードするのに一般的なバッファー DMA を使用します。 一般的なバッファーでは、連続しているし、ホストの CPU と、デバイスの両方にアクセス可能では常にします。

    共通のバッファーは、貴重なシステム リソースです。 適切な全体的なドライバーとシステムのパフォーマンスは、ドライバーはできるだけ経済的な共通バッファー DMA を使用する必要があります。

、バス マスター アダプターの性質に応じてミニポート ドライバーによってパケットに基づく DMA を排他的に使用して、排他的に一般的なバッファー DMA を使用して他のユーザー両方を使用していくつか。

DMA の種類を使用するに関係なく、ミニポート ドライバーを呼び出す必要があります[ **VideoPortGetDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff570312)へのポインターを取得する、 [**担当副社長\_DMA\_アダプター** ](https://msdn.microsoft.com/library/windows/hardware/ff570570)構造体し、後続の DMA 関数の呼び出しに対して使用します。 ミニポート ドライバーを呼び出す必要がありますの DMA 操作を継続的な必要がなくなったとき[ **VideoPortPutDmaAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff570335)をそのアダプタ オブジェクトを破棄します。

次のサブセクションでは、ビデオ ポート ドライバーによって提供されるパケットに基づくと、一般的なバッファーの DMA サポートを使用する方法について説明します。

[バス マスター DMA のパケットに基づく](packet-based-bus-master-dma.md)

[一般的なバッファーのバス マスター DMA](common-buffer-bus-master-dma.md)

[DMA を使用する場合に考慮すべき点](points-to-consider-when-using-dma.md)

 

 





