---
title: PROPSETID\_しました\_VIDEODECODER
description: PROPSETID\_しました\_VIDEODECODER
ms.assetid: 86b581b7-51fd-4662-8291-4c5baf9d3b16
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97b413a1eac496ff8ab05518b6570cb941f2788f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527299"
---
# <a name="propsetidvidcapvideodecoder"></a>PROPSETID\_しました\_VIDEODECODER


## <span id="ddk_propsetid_vidcap_videodecoder_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEODECODER_KS"></span>


PROPSETID\_しました\_VIDEODECODER プロパティ コントロールをアナログ ビデオ デコーダーのデバイスに設定します。 アナログのビデオ デコーダーでは、RGB など YUV をデジタル形式にベースバンド アナログ ビデオ信号に変換します。

KSPROPERTY\_しました\_VIDEODECODER 列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、アナログ ビデオ キャプチャ デバイスでのみ実装する必要があります。

ビデオ キャプチャ ミニドライバーは、次のプロパティを実装するために必要です。

[**KSPROPERTY\_VIDEODECODER\_キャップ**](ksproperty-videodecoder-caps.md)

[**KSPROPERTY\_VIDEODECODER\_標準**](ksproperty-videodecoder-standard.md)

[**KSPROPERTY\_VIDEODECODER\_状態**](ksproperty-videodecoder-status.md)

ビデオ キャプチャ ミニドライバーは、必要に応じて、次のプロパティを実装可能性があります。

[**KSPROPERTY\_VIDEODECODER\_出力\_を有効にします。**](ksproperty-videodecoder-output-enable.md)

[**KSPROPERTY\_VIDEODECODER\_VCR\_タイミング**](ksproperty-videodecoder-vcr-timing.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMAnalogVideoDecoder**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





