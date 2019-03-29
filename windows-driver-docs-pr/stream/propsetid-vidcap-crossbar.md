---
title: PROPSETID\_しました\_クロスバー
description: PROPSETID\_しました\_クロスバー
ms.assetid: a2ed126c-75ee-4346-845e-9f675ca34416
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7549c59fae62b8a0af905aa2ccce1244a23eac8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569707"
---
# <a name="propsetidvidcapcrossbar"></a>PROPSETID\_しました\_クロスバー


## <span id="ddk_propsetid_vidcap_crossbar_ks"></span><span id="DDK_PROPSETID_VIDCAP_CROSSBAR_KS"></span>


PROPSETID\_しました\_クロスバー プロパティは、ビデオおよびオーディオ信号をルーティングするコントロールにデバイスを設定します。 クロスバーは、入力の N と M の出力の一般的な切り替えマトリックス上にモデル化されます。 実際のハードウェア実装は、この一般的なルーティング機能のサブセットのみを許可することがありますが、入力信号のいずれかの出力の 1 つ以上にルーティングされることができます。 アナログまたはデジタル信号をルーティングするクロスバーを使用できます。 1 つクロスバーはビデオとオーディオの両方の信号をルーティングできます。 必要に応じてビデオ ピンは、ビデオの pin に関連付けられているオーディオの pin を指定できます。

KSPROPERTY\_しました\_クロスバー列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、ミニドライバー クロスバー デバイスのによってのみ実装する必要があります。

クロスバー キャプチャ ミニドライバーは、次のプロパティを実装するために必要です。

[**KSPROPERTY\_クロスバー\_できます\_ルート**](ksproperty-crossbar-can-route.md)

[**KSPROPERTY\_クロスバー\_キャップ**](ksproperty-crossbar-caps.md)

[**KSPROPERTY\_クロスバー\_PININFO**](ksproperty-crossbar-pininfo.md)

[**KSPROPERTY\_クロスバー\_ルート**](ksproperty-crossbar-route.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMCrossbar**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





