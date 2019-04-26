---
title: PROPSETID\_しました\_TVAUDIO
description: PROPSETID\_しました\_TVAUDIO
ms.assetid: 33c76f30-2e4b-48b7-a463-f6363419dca3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35eba440585299c5e9a26b1c28b142cf9e9d3455
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349111"
---
# <a name="propsetidvidcaptvaudio"></a>PROPSETID\_しました\_TVAUDIO


## <span id="ddk_propsetid_vidcap_tvaudio_ks"></span><span id="DDK_PROPSETID_VIDCAP_TVAUDIO_KS"></span>


PROPSETID\_しました\_TVAUDIO プロパティは、テレビのソースに関連付けられているオーディオに固有の設定を制御します。 これには、セカンダリ オーディオ プログラム (SAP) とステレオまたは mono の選択が含まれます。 これらのコントロールは通常、デバイスで見つかったシステム オーディオ ミキサーに外部。

KSPROPERTY\_しました\_TVAUDIO 列挙体*ksmedia.h*このセットのプロパティを指定します。

サポートこのプロパティを設定は省略可能なテレビのオーディオをサポートするデバイスのミニドライバーによってのみ実装する必要があります。

テレビ オーディオ キャプチャ ミニドライバーは、次のプロパティを実装するために必要です。

[**KSPROPERTY\_TVAUDIO\_キャップ**](ksproperty-tvaudio-caps.md)

[**KSPROPERTY\_TVAUDIO\_CURRENTLY\_AVAILABLE\_MODES**](ksproperty-tvaudio-currently-available-modes.md)

[**KSPROPERTY\_TVAUDIO\_モード**](ksproperty-tvaudio-mode.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMTVAudio**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





