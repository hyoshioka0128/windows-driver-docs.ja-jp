---
title: ピクセル単位でのフォグ濃度のクランプ
description: ピクセル単位でのフォグ濃度のクランプ
ms.assetid: 249d085a-b54c-48b3-bc7a-3fe5f8238b1b
keywords:
- WDK DirectX 9.0 ピクセルあたり霧強度をクランプ
- WDK DirectX 9.0 ピクセルあたり霧強度
- WDK DirectX 9.0 をクランプ ピクセル霧の強度
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfbd86db9c30804eb9cf9b48fb0cb42eaee09aa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354328"
---
# <a name="clamping-fog-intensity-per-pixel"></a>ピクセル単位でのフォグ濃度のクランプ


## <span id="ddk_clamping_fog_intensity_per_pixel_gg"></span><span id="DDK_CLAMPING_FOG_INTENSITY_PER_PIXEL_GG"></span>


2.0 以降のピクセルまたは頂点シェーダーのバージョンをサポートするデバイスの DirectX 9.0 バージョンのドライバーがそのデバイスには、D3DPMISCCAPS を設定して、ピクセル単位で霧輝度値をクランプがサポートしているを指定する必要があります\_FOGINFVF 機能ビット。 デバイスでは保存されませんフォグ係数反射のアルファ チャネル ソフトウェア頂点シェーダーを使用するときにユーザーに通知されます。 デバイスは、ピクセル処理ユニットの頂点ごとの霧の輝度値とアルファ チャネルを常に上書きする代わりに (固定関数頂点のパイプラインで計算されます)、スペキュラ色のアルファ チャネルを渡すことができます。

霧輝度値をクランプします。 ピクセル単位で、ドライバー、ため、DirectX 9.0 と不要になった後で、ランタイムは、ドライバーに送信する前に霧輝度値をクランプします。

ドライバーは、確認の場合、霧値を取得する方法を決定します。、D3DFVF\_柔軟な頂点の形式 (FVF) で霧ビットが設定されます。 場合 D3DFVF\_霧の設定、ドライバーは、頂点ごとに渡される個別の霧値を取得します。 場合 D3DFVF\_霧が設定されていないと、ドライバーは霧を使用する必要があります、ドライバーは、反射色のアルファ チャネルからフォグ値を取得します。

ドライバーが D3DPMISCCAPS を設定するときに\_FOGINFVF、ランタイムはさらに、D3DPMISCCAPS 設定\_FOGANDSPECULARALPHA 機能ビット、 **PrimitiveMiscCaps** D3DCAPS9 構造体のメンバー。

 

 





