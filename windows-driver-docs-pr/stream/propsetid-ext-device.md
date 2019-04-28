---
title: PROPSETID\_EXT\_デバイス
description: PROPSETID\_EXT\_デバイス
ms.assetid: fe1a14dc-b337-462b-ac2a-10eef036ef7f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cd96de0d8bd0eb7a34fa9a8e087e6005cf4182e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362192"
---
# <a name="propsetidextdevice"></a>PROPSETID\_EXT\_デバイス


## <span id="ddk_propsetid_ext_device_ks"></span><span id="DDK_PROPSETID_EXT_DEVICE_KS"></span>


PROPSETID\_EXT\_デバイス プロパティは、コントロール ミニ DV カメラなどの外部のデバイスを設定します。

KSPROPERTY\_EXTDEVICE 列挙体*ksmedia.h*このセットのプロパティを指定します。

このプロパティを設定は省略可能と外部のビデオ キャプチャ デバイスをサポートするミニドライバーによってのみ実装する必要をサポートします。

[**KSPROPERTY\_EXTDEVICE\_ID**](ksproperty-extdevice-id.md)

[**KSPROPERTY\_EXTDEVICE\_バージョン**](ksproperty-extdevice-version.md)

[**KSPROPERTY\_EXTDEVICE\_POWER\_状態**](ksproperty-extdevice-power-state.md)

[**KSPROPERTY\_EXTDEVICE\_ポート**](ksproperty-extdevice-port.md)

[**KSPROPERTY\_EXTDEVICE\_機能**](ksproperty-extdevice-capabilities.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow インターフェイス

DirectShow **IAMExtDevice**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft Windows SDK の DirectShow のドキュメントを参照してください)。

 

 





