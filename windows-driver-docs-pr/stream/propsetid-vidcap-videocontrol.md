---
title: PROPSETID\_しました\_VIDEOCONTROL
description: PROPSETID\_しました\_VIDEOCONTROL
ms.assetid: 892663c1-a807-4d03-9af0-f065149e7d42
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bb5c9851e41e63293133c5abdf2e261cf2e5bf4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549276"
---
# <a name="propsetidvidcapvideocontrol"></a>PROPSETID\_しました\_VIDEOCONTROL


## <span id="ddk_propsetid_vidcap_videocontrol_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOCONTROL_KS"></span>


PROPOSETID\_しました\_VIDEOCONTROL プロパティが使用可能なフレーム レートとイメージの向きを列挙するなどのビデオ キャプチャ操作の補足的な側面をコントロールに設定します。 一般に、アナログのデジタイザーでは、USB と 1394 会議用カメラ サポートしますが、制限されたフレーム レートの設定をすべてのフレーム レートの要求をサポートできます。

KSPROPERTY\_しました\_VIDEOCONTROL 列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、ミニドライバーの任意のフレーム レートでビデオをキャプチャできないデバイスでのみ実装する必要があります。

ビデオ キャプチャ ミニドライバーは、次のプロパティを実装するために必要です。

[**KSPROPERTY\_VIDEOCONTROL\_キャップ**](ksproperty-videocontrol-caps.md)

ビデオ キャプチャ ミニドライバーは、必要に応じて、次のプロパティを実装可能性があります。

[**KSPROPERTY\_VIDEOCONTROL\_実際\_フレーム\_率**](ksproperty-videocontrol-actual-frame-rate.md)

[**KSPROPERTY\_VIDEOCONTROL\_フレーム\_料金**](ksproperty-videocontrol-frame-rates.md)

[**KSPROPERTY\_VIDEOCONTROL\_モード**](ksproperty-videocontrol-mode.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

このプロパティ セットへのアクセスを提供する DirectShow インターフェイスはありません。

 

 





