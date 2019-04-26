---
title: PROPSETID\_しました\_拡張子\_単位
description: PROPSETID\_しました\_拡張子\_単位
ms.assetid: 7aa4742f-e64f-4798-a9e0-8c1f02aa15b3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545dfbed3135e108e0bdc9fb5823eb92c56a1cc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349113"
---
# <a name="propsetidvidcapextensionunit"></a>PROPSETID\_しました\_拡張子\_単位


## <span id="ddk_propsetid_vidcap_extension_unit_ks"></span><span id="DDK_PROPSETID_VIDCAP_EXTENSION_UNIT_KS"></span>


PROPSETID\_しました\_拡張子\_単位のプロパティ セットで使用するための新しい、 [USB ビデオ クラス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff568649)します。

このプロパティ セットは、ベンダー固有の拡張機能単位を実装しているデバイスでサポートされます。 プロパティのベンダーから提供されたページとアプリケーションは、ジェネリックを使用して設定でこのプロパティをアクセス[IKsControl](https://msdn.microsoft.com/library/windows/hardware/ff559766) COM インターフェイスです。

KSPROPERTY\_拡張子\_単位列挙で*ksmedia.h*このセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、ベンダー定義のハードウェアの制御を提供しているデバイスでのみ実装する必要があります。

USB ビデオ クラス ドライバーのクライアントは、フィルターまたはノードの次の要求を行うことができます。

[**KSPROPERTY\_拡張子\_単位\_情報**](ksproperty-extension-unit-info.md)

### <a name="span-iddirectshowinterfacesspanspan-iddirectshowinterfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow インターフェイス

このセットのプロパティにアクセスするのにには、次のユーザー モード インターフェイスを使用します。**IKsTopologyInfo**、 **ISelector**、および**IKsNodeControl**します。 これらのインターフェイスについては、Microsoft Windows SDK、DirectShow のドキュメントを参照してください。

 

 





