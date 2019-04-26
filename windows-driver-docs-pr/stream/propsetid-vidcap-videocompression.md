---
title: PROPSETID\_しました\_VIDEOCOMPRESSION
description: PROPSETID\_しました\_VIDEOCOMPRESSION
ms.assetid: 7af6f7f0-d446-4b44-9423-efd37f731e0b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c4b7bea33a0f37fe006bd7e4fea498966d13b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349112"
---
# <a name="propsetidvidcapvideocompression"></a>PROPSETID\_しました\_VIDEOCOMPRESSION


## <span id="ddk_propsetid_vidcap_videocompression_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOCOMPRESSION_KS"></span>


PROPSETID\_しました\_VIDEOCOMPRESSION プロパティは、デバイスのビデオの圧縮設定コントロールを設定します。

KSPROPERTY\_しました\_VIDEOCOMPRESSION 列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、ビデオの圧縮コーデックを実装しているデバイスでのみ実装する必要があります。

ビデオ キャプチャ ミニドライバーは、次のプロパティを実装するために必要です。

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO**](ksproperty-videocompression-getinfo.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_キーフレーム\_率**](ksproperty-videocompression-keyframe-rate.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_フレーム\_サイズ**](ksproperty-videocompression-override-frame-size.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_キーフレーム**](ksproperty-videocompression-override-keyframe.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_1 秒あたり\_キーフレーム**](ksproperty-videocompression-pframes-per-keyframe.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_品質**](ksproperty-videocompression-quality.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_WINDOWSIZE**](ksproperty-videocompression-windowsize.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMVideoCompression**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





