---
title: PROPSETID\_しました\_セレクター
description: PROPSETID\_しました\_セレクター
ms.assetid: a7328f22-be49-48ac-b923-15f66dc38ccb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3366447bd162cdefe577ccc12c4b31026cac9f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385699"
---
# <a name="propsetidvidcapselector"></a>PROPSETID\_しました\_セレクター


## <span id="ddk_propsetid_vidcap_selector_ks"></span><span id="DDK_PROPSETID_VIDCAP_SELECTOR_KS"></span>


PROPSETID\_しました\_セレクター プロパティの設定は新しいで使用するため、 [USB ビデオ クラス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)します。 このプロパティのセットには実装するために必要なプロパティが含まれています、 **ISelector**インターフェイス (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

KSPROPERTY\_しました\_セレクター列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティは、レンズの入力を提供する現在のノードのコントロールを設定します。 このプロパティ セットのサポートは省略可能で、これらのコントロールを提供しているデバイスでのみ実装する必要があります。

USB ビデオ クラス ドライバーのクライアントは、フィルターまたはノードの次の要求を行うことができます。

[**KSPROPERTY\_セレクター\_ソース\_ノード\_ID**](ksproperty-selector-source-node-id.md)

[**KSPROPERTY\_NUM\_ソース**](ksproperty-num-sources.md)

### <a name="span-iddirectshowinterfacesspanspan-iddirectshowinterfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow インターフェイス

プロパティで、PROPSETID\_しました\_セレクター プロパティ セットには、DirectShow を通じてアクセス**ISelector**インターフェイス (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





