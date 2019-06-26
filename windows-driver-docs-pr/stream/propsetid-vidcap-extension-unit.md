---
title: PROPSETID\_しました\_拡張子\_単位
description: PROPSETID\_しました\_拡張子\_単位
ms.assetid: 7aa4742f-e64f-4798-a9e0-8c1f02aa15b3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5471b3d12202abc7dfd54635392309833c6e532
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379057"
---
# <a name="propsetidvidcapextensionunit"></a>PROPSETID\_しました\_拡張子\_単位


## <span id="ddk_propsetid_vidcap_extension_unit_ks"></span><span id="DDK_PROPSETID_VIDCAP_EXTENSION_UNIT_KS"></span>


PROPSETID\_しました\_拡張子\_単位のプロパティ セットで使用するための新しい、 [USB ビデオ クラス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)します。

このプロパティ セットは、ベンダー固有の拡張機能単位を実装しているデバイスでサポートされます。 プロパティのベンダーから提供されたページとアプリケーションは、ジェネリックを使用して設定でこのプロパティをアクセス[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol) COM インターフェイスです。

KSPROPERTY\_拡張子\_単位列挙で*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、ベンダー定義のハードウェアの制御を提供しているデバイスでのみ実装する必要があります。

USB ビデオ クラス ドライバーのクライアントは、フィルターまたはノードの次の要求を行うことができます。

[**KSPROPERTY\_拡張子\_単位\_情報**](ksproperty-extension-unit-info.md)

### <a name="span-iddirectshowinterfacesspanspan-iddirectshowinterfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow インターフェイス

このセットのプロパティにアクセスするのにには、次のユーザー モード インターフェイスを使用します。**IKsTopologyInfo**、 **ISelector**、および**IKsNodeControl**します。 これらのインターフェイスについては、Microsoft Windows SDK、DirectShow のドキュメントを参照してください。

 

 





