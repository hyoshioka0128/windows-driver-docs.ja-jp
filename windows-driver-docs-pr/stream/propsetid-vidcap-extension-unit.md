---
title: PROPSETID\_VIDCAP\_EXTENSION\_UNIT
description: PROPSETID\_VIDCAP\_EXTENSION\_UNIT
ms.assetid: 7aa4742f-e64f-4798-a9e0-8c1f02aa15b3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea91bcafc546844181194ab2534128a45f087eb2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845306"
---
# <a name="propsetid_vidcap_extension_unit"></a>PROPSETID\_VIDCAP\_EXTENSION\_UNIT


## <span id="ddk_propsetid_vidcap_extension_unit_ks"></span><span id="DDK_PROPSETID_VIDCAP_EXTENSION_UNIT_KS"></span>


PROPSETID\_VIDCAP\_EXTENSION\_UNIT プロパティセットは、 [USB ビデオクラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)で使用するための新しいものです。

このプロパティセットは、ベンダー固有の拡張機能ユニットを実装するデバイスでサポートされています。 ベンダーが提供するプロパティページとアプリケーションは、ジェネリック[Iksk コントロール](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)COM インターフェイスを使用して、このプロパティにアクセスします。

Ksproperty では、KSK プロパティ\_EXTENSION\_UNIT 列挙体が、このセットのプロパティを指定し*ます。*

このプロパティセットのサポートは省略可能であり、ベンダーが定義したハードウェア制御を提供するデバイスによってのみ実装する必要があります。

USB video クラスドライバーのクライアントは、次のフィルターまたはノードの要求を行うことができます。

[**KSK プロパティ\_拡張機能\_ユニット\_情報**](ksproperty-extension-unit-info.md)

### <a name="span-iddirectshow_interfacesspanspan-iddirectshow_interfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow インターフェイス

次のユーザーモードインターフェイスを使用して、このセットのプロパティにアクセスします: **IKsTopologyInfo**、 **iselector**、および**IKsNodeControl**。 これらのインターフェイスの詳細については、Microsoft Windows SDK の DirectShow のドキュメントを参照してください。

 

 





