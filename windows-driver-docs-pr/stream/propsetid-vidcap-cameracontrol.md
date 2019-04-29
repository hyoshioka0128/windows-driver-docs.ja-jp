---
title: PROPSETID\_しました\_CAMERACONTROL
description: PROPSETID\_しました\_CAMERACONTROL
ms.assetid: 8899a474-fa6f-4d5c-bd68-2433428bb5c5
keywords:
- KSPROPERTY_VIDCAP_CAMERACONTROL
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54231c135b9d3cc27eacfe345b2fb3e2760e6867
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387111"
---
# <a name="propsetidvidcapcameracontrol"></a>PROPSETID\_しました\_CAMERACONTROL


## <span id="ddk_propsetid_vidcap_cameracontrol_ks"></span><span id="DDK_PROPSETID_VIDCAP_CAMERACONTROL_KS"></span>


PROPSETID\_しました\_CAMERACONTROL プロパティはデバイスのカメラ設定コントロールを設定します。 コントロールについては、ITU T.RDC 標準のサブセットです。

KSPROPERTY\_しました\_Ksmedia.h CAMERACONTROL 列挙体がこのセットのプロパティを指定します。

このプロパティ セットのサポートは省略可能で、カメラ コントロールの設定を提供しているデバイスのミニドライバーによってのみ実装する必要があります。 詳細については、次を参照してください。、 [ITU](https://go.microsoft.com/fwlink/p/?linkid=8741) web サイト。

USB ビデオ クラスでは、前に、この列挙体には、次のプロパティが含まれています。

[**KSPROPERTY\_CAMERACONTROL\_露出**](ksproperty-cameracontrol-exposure.md)

[**KSPROPERTY\_CAMERACONTROL\_フォーカス**](ksproperty-cameracontrol-focus.md)

[**KSPROPERTY\_CAMERACONTROL\_IRIS**](ksproperty-cameracontrol-iris.md)

[**KSPROPERTY\_CAMERACONTROL\_ズーム**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY\_CAMERACONTROL\_方向へパンします。**](ksproperty-cameracontrol-pan.md)

[**KSPROPERTY\_CAMERACONTROL\_ロール**](ksproperty-cameracontrol-roll.md)

[**KSPROPERTY\_CAMERACONTROL\_傾き**](ksproperty-cameracontrol-tilt.md)

導入に伴い、 [USB ビデオ クラス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff568649)、次のプロパティは、KSPROPERTY に追加された\_しました\_CAMERACONTROL 列挙体。 Windows Vista および Windows の以降のバージョンでは、これらのプロパティがサポートされています。

[**KSPROPERTY\_CAMERACONTROL\_SCANMODE**](ksproperty-cameracontrol-scanmode.md)

[**KSPROPERTY\_CAMERACONTROL\_プライバシー**](ksproperty-cameracontrol-privacy.md)

[**KSPROPERTY\_CAMERACONTROL\_PANTILT**](ksproperty-cameracontrol-pantilt.md)

[**KSPROPERTY\_CAMERACONTROL\_パン\_相対**](ksproperty-cameracontrol-pan-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_傾き\_相対**](ksproperty-cameracontrol-tilt-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_ロール\_相対**](ksproperty-cameracontrol-roll-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_ズーム\_相対**](ksproperty-cameracontrol-zoom-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_露出\_相対**](ksproperty-cameracontrol-exposure-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_IRIS\_相対**](ksproperty-cameracontrol-iris-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_フォーカス\_相対**](ksproperty-cameracontrol-focus-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_PANTILT\_相対**](ksproperty-cameracontrol-pantilt-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_焦点\_長さ**](ksproperty-cameracontrol-focal-length.md)

[**KSPROPERTY\_CAMERACONTROL\_自動\_露出\_優先順位**](ksproperty-cameracontrol-auto-exposure-priority.md)

DirectShow **IAMCameraControl**インターフェイスには、このセットのプロパティへのアクセスが用意されています (Microsoft DirectShow のドキュメントで、Windows ソフトウェア開発キット (SDK) を参照してください)。

## <a name="span-idwindows8extendedcameracontrolpropertiesspanspan-idwindows8extendedcameracontrolpropertiesspanspan-idwindows8extendedcameracontrolpropertiesspanwindows8-extended-camera-control-properties"></a><span id="Windows_8_extended_camera_control_properties"></span><span id="windows_8_extended_camera_control_properties"></span><span id="WINDOWS_8_EXTENDED_CAMERA_CONTROL_PROPERTIES"></span>Windows 8 がカメラ コントロールのプロパティを拡張


Windows 8 以降、これらの追加プロパティは、カメラのコントロールの設定を取得またはユーザー モードのクライアントでサポートされます。

[**KSPROPERTY\_CAMERACONTROL\_FLASH\_プロパティ**](ksproperty-cameracontrol-flash-property.md)

[**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_S**](https://msdn.microsoft.com/library/windows/hardware/jj553707)

[**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_プロパティ**](ksproperty-cameracontrol-region-of-interest-property.md)

[**KSPROPERTY\_CAMERACONTROL\_ビデオ\_安定化\_モード\_プロパティ**](ksproperty-cameracontrol-video-stabilization-mode-property.md)

 

 





