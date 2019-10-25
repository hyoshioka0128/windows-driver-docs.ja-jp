---
title: PROPSETID\_VIDCAP\_CAMERACONTROL
description: PROPSETID\_VIDCAP\_CAMERACONTROL
ms.assetid: 8899a474-fa6f-4d5c-bd68-2433428bb5c5
keywords:
- KSPROPERTY_VIDCAP_CAMERACONTROL
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87102b025557ca5069915795ba45a601e78d6afc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823726"
---
# <a name="propsetid_vidcap_cameracontrol"></a>PROPSETID\_VIDCAP\_CAMERACONTROL


## <span id="ddk_propsetid_vidcap_cameracontrol_ks"></span><span id="DDK_PROPSETID_VIDCAP_CAMERACONTROL_KS"></span>


PROPSETID\_VIDCAP\_CAMERACONTROL プロパティセットは、カメラのデバイス設定を制御します。 このコントロールによって提供されるコントロールは、ITU-T 標準のサブセットです。

Ksk プロパティ\_VIDCAP\_CAMERACONTROL 列挙体は、このセットのプロパティを指定します。

このプロパティセットのサポートは省略可能であり、カメラコントロール設定を提供するデバイスのミニドライバーのみが実装する必要があります。 詳細については、 [ITU](https://go.microsoft.com/fwlink/p/?linkid=8741)の web サイトを参照してください。

USB ビデオクラスより前では、この列挙体には次のプロパティが含まれていました。

[**KSK プロパティ\_CAMERACONTROL\_の公開**](ksproperty-cameracontrol-exposure.md)

[**KSK プロパティ\_CAMERACONTROL\_フォーカス**](ksproperty-cameracontrol-focus.md)

[**KSK プロパティ\_CAMERACONTROL\_虹彩**](ksproperty-cameracontrol-iris.md)

[**KSK プロパティ\_CAMERACONTROL\_ZOOM**](ksproperty-cameracontrol-zoom.md)

[**KSK プロパティ\_CAMERACONTROL\_PAN**](ksproperty-cameracontrol-pan.md)

[**KSK プロパティ\_CAMERACONTROL\_ROLL**](ksproperty-cameracontrol-roll.md)

[**KSK プロパティ\_CAMERACONTROL\_チルト**](ksproperty-cameracontrol-tilt.md)

[USB ビデオクラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)の導入により、次のプロパティが ksk プロパティ\_VIDCAP\_CAMERACONTROL 列挙型に追加されました。 Windows Vista 以降のバージョンの Windows では、次のプロパティがサポートされています。

[**KSPROPERTY\_CAMERACONTROL\_SCANMODE**](ksproperty-cameracontrol-scanmode.md)

[**KSK プロパティ\_CAMERACONTROL\_PRIVACY**](ksproperty-cameracontrol-privacy.md)

[**KSK プロパティ\_CAMERACONTROL\_PANTILT**](ksproperty-cameracontrol-pantilt.md)

[**KSK プロパティ\_CAMERACONTROL\_パン\_相対**](ksproperty-cameracontrol-pan-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_傾き\_相対**](ksproperty-cameracontrol-tilt-relative.md)

[**KSK プロパティ\_CAMERACONTROL\_ROLL\_相対**](ksproperty-cameracontrol-roll-relative.md)

[**KSK プロパティ\_CAMERACONTROL\_ZOOM\_相対**](ksproperty-cameracontrol-zoom-relative.md)

[**KSK プロパティ\_CAMERACONTROL\_露出\_相対的**](ksproperty-cameracontrol-exposure-relative.md)

[**KSK プロパティ\_CAMERACONTROL\_虹彩\_相対**](ksproperty-cameracontrol-iris-relative.md)

[**KSK プロパティ\_CAMERACONTROL\_フォーカス\_相対**](ksproperty-cameracontrol-focus-relative.md)

[**KSK プロパティ\_CAMERACONTROL\_PANTILT\_相対**](ksproperty-cameracontrol-pantilt-relative.md)

[**KSK プロパティ\_CAMERACONTROL\_焦点\_の長さ**](ksproperty-cameracontrol-focal-length.md)

[**KSK プロパティ\_CAMERACONTROL\_自動\_露出\_優先度**](ksproperty-cameracontrol-auto-exposure-priority.md)

DirectShow **IAMCameraControl**インターフェイス (Windows Software Development KIT (SDK) の Microsoft DirectShow ドキュメントを参照) は、このセットのプロパティへのアクセスを提供します。

## <a name="span-idwindows_8_extended_camera_control_propertiesspanspan-idwindows_8_extended_camera_control_propertiesspanspan-idwindows_8_extended_camera_control_propertiesspanwindows8-extended-camera-control-properties"></a><span id="Windows_8_extended_camera_control_properties"></span><span id="windows_8_extended_camera_control_properties"></span><span id="WINDOWS_8_EXTENDED_CAMERA_CONTROL_PROPERTIES"></span>Windows 8 拡張カメラコントロールのプロパティ


Windows 8 以降では、ユーザーモードクライアントでカメラのコントロール設定を取得または設定するために、次の追加のプロパティがサポートされています。

[**KSK プロパティ\_CAMERACONTROL\_FLASH\_プロパティ**](ksproperty-cameracontrol-flash-property.md)

[**KSK プロパティ\_CAMERACONTROL\_IMAGE\_PIN\_機能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

[**KSK プロパティ\_CAMERACONTROL\_REGION\_\_関心のある\_プロパティ**](ksproperty-cameracontrol-region-of-interest-property.md)

[**KSPROPERTY\_CAMERACONTROL\_VIDEO\_安定化\_MODE\_プロパティ**](ksproperty-cameracontrol-video-stabilization-mode-property.md)

 

 





