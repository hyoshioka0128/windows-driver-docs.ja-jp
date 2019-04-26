---
title: PROPSETID\_チューナー
description: PROPSETID\_チューナー
ms.assetid: 2697fb71-32da-40d0-aebf-d91b1a0587ba
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66be9e3183620e9bee2011e23eae0877db773abb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342150"
---
# <a name="propsetidtuner"></a>PROPSETID\_チューナー


## <span id="ddk_propsetid_tuner_ks"></span><span id="DDK_PROPSETID_TUNER_KS"></span>


PROPSETID\_チューナー プロパティは、そのサポートのテレビやラジオのチューニングにコントロールのデバイスを設定します。 このプロパティ セットは、multistandard のビデオ チューナーとチューナーを複数の入力をサポートします。

KSPROPERTY\_でチューナー列挙*ksmedia.h*このセットのプロパティを指定します。

このプロパティを設定は省略可能、テレビやラジオのチューニングをサポートするミニドライバーによってのみ実装する必要をサポートします。

チューナー キャプチャ ミニドライバーは、次のプロパティを実装するために必要です。

[**KSPROPERTY\_チューナー\_キャップ**](ksproperty-tuner-caps.md)

[**KSPROPERTY\_チューナー\_頻度**](ksproperty-tuner-frequency.md)

[**KSPROPERTY\_チューナー\_入力**](ksproperty-tuner-input.md)

[**KSPROPERTY\_チューナー\_モード**](ksproperty-tuner-mode.md)

[**KSPROPERTY\_チューナー\_モード\_キャップ**](ksproperty-tuner-mode-caps.md)

[**KSPROPERTY\_チューナー\_スキャン\_CAP** ](ksproperty-tuner-scan-caps.md) Windows Vista の新機能

[**KSPROPERTY\_チューナー\_標準**](ksproperty-tuner-standard.md)

[**KSPROPERTY\_チューナー\_状態**](ksproperty-tuner-status.md)

チューナー キャプチャ ミニドライバーは、次のプロパティを必要に応じて実装できます。

[**KSPROPERTY\_チューナー\_場合\_中**](ksproperty-tuner-if-medium.md)

[**KSPROPERTY\_チューナー\_NETWORKTYPE\_スキャン\_CAP** ](ksproperty-tuner-networktype-scan-caps.md) Windows Vista の新機能

[**KSPROPERTY\_チューナー\_スキャン\_状態**](ksproperty-tuner-scan-status.md) Windows Vista の新機能

[**KSPROPERTY\_チューナー\_標準\_モード**](ksproperty-tuner-standard-mode.md) Windows Vista の新機能

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMTVTuner**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





