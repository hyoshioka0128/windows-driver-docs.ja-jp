---
title: PROPSETID\_しました\_セレクター
description: PROPSETID\_しました\_セレクター
ms.assetid: a7328f22-be49-48ac-b923-15f66dc38ccb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 791acde249a4568c3db1711255d6dd04660be45c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385170"
---
# <a name="propsetidvidcapselector"></a>PROPSETID\_しました\_セレクター


## <span id="ddk_propsetid_vidcap_selector_ks"></span><span id="DDK_PROPSETID_VIDCAP_SELECTOR_KS"></span>


PROPSETID\_しました\_セレクター プロパティの設定は新しいで使用するため、 [USB ビデオ クラス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff568649)します。 このプロパティのセットには実装するために必要なプロパティが含まれています、 **ISelector**インターフェイス (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

KSPROPERTY\_しました\_セレクター列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティは、レンズの入力を提供する現在のノードのコントロールを設定します。 このプロパティ セットのサポートは省略可能で、これらのコントロールを提供しているデバイスでのみ実装する必要があります。

USB ビデオ クラス ドライバーのクライアントは、フィルターまたはノードの次の要求を行うことができます。

[**KSPROPERTY\_セレクター\_ソース\_ノード\_ID**](ksproperty-selector-source-node-id.md)

[**KSPROPERTY\_NUM\_ソース**](ksproperty-num-sources.md)

### <a name="span-iddirectshowinterfacesspanspan-iddirectshowinterfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow インターフェイス

プロパティで、PROPSETID\_しました\_セレクター プロパティ セットには、DirectShow を通じてアクセス**ISelector**インターフェイス (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





