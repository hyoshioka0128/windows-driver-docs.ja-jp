---
title: PROPSETID \_ VIDCAP \_ CAMERACONTROL
description: PROPSETID \_ VIDCAP \_ CAMERACONTROL
ms.assetid: 8899a474-fa6f-4d5c-bd68-2433428bb5c5
keywords:
- KSPROPERTY_VIDCAP_CAMERACONTROL
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9b08f2c802c26a96187a02b24dd3fee8e7e09ec3
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073437"
---
# <a name="propsetid_vidcap_cameracontrol"></a>PROPSETID \_ VIDCAP \_ CAMERACONTROL

PROPSETID \_ VIDCAP \_ CAMERACONTROL プロパティセットは、カメラのデバイス設定を制御します。 このコントロールによって提供されるコントロールは、ITU-T 標準のサブセットです。

\_ \_ Ksproperty. h の ksk プロパティ VIDCAP CAMERACONTROL 列挙体は、このセットのプロパティを指定します。

このプロパティセットのサポートは省略可能であり、カメラコントロール設定を提供するデバイスのミニドライバーのみが実装する必要があります。 詳細については、 [ITU](https://www.itu.int/)の web サイトを参照してください。

USB ビデオクラスより前では、この列挙体には次のプロパティが含まれていました。

[**KSPROPERTY \_ CAMERACONTROL の \_ 公開**](ksproperty-cameracontrol-exposure.md)

[**KSPROPERTY \_ CAMERACONTROL \_ フォーカス**](ksproperty-cameracontrol-focus.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 虹彩**](ksproperty-cameracontrol-iris.md)

[**KSK プロパティ \_ CAMERACONTROL \_ ZOOM**](ksproperty-cameracontrol-zoom.md)

[**KSK プロパティ \_ CAMERACONTROL \_ PAN**](ksproperty-cameracontrol-pan.md)

[**KSK プロパティ \_ CAMERACONTROL \_ ROLL**](ksproperty-cameracontrol-roll.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 傾き**](ksproperty-cameracontrol-tilt.md)

[USB ビデオクラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)の導入により、次のプロパティが ksk プロパティ \_ VIDCAP CAMERACONTROL 列挙に追加されました \_ 。

[**KSPROPERTY \_ CAMERACONTROL \_ SCANMODE**](ksproperty-cameracontrol-scanmode.md)

[**KSK プロパティ \_ CAMERACONTROL の \_ プライバシー**](ksproperty-cameracontrol-privacy.md)

[**KSPROPERTY \_ CAMERACONTROL \_ PANTILT**](ksproperty-cameracontrol-pantilt.md)

[**KSK プロパティ \_ CAMERACONTROL \_ パン \_ 相対**](ksproperty-cameracontrol-pan-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 傾き \_ 相対**](ksproperty-cameracontrol-tilt-relative.md)

[**KSK プロパティ \_ CAMERACONTROL \_ ロール \_ 相対**](ksproperty-cameracontrol-roll-relative.md)

[**KSK プロパティ \_ CAMERACONTROL \_ ZOOM \_ 相対値**](ksproperty-cameracontrol-zoom-relative.md)

[**KSK プロパティ \_ CAMERACONTROL \_ 露出の \_ 相対値**](ksproperty-cameracontrol-exposure-relative.md)

[**KSK プロパティ \_ CAMERACONTROL \_ 虹彩の \_ 相対値**](ksproperty-cameracontrol-iris-relative.md)

[**KSK プロパティ \_ CAMERACONTROL \_ の \_ 相対的なフォーカス**](ksproperty-cameracontrol-focus-relative.md)

[**KSK プロパティ \_ CAMERACONTROL \_ PANTILT \_ 相対値**](ksproperty-cameracontrol-pantilt-relative.md)

[**KSPROPERTY \_ CAMERACONTROL の \_ 焦点の \_ 長さ**](ksproperty-cameracontrol-focal-length.md)

[**KSK プロパティ \_ CAMERACONTROL の \_ 自動 \_ 露出の \_ 優先度**](ksproperty-cameracontrol-auto-exposure-priority.md)

DirectShow **IAMCameraControl**インターフェイス (Windows Software Development KIT (SDK) の Microsoft DirectShow ドキュメントを参照) は、このセットのプロパティへのアクセスを提供します。

## <a name="windows8-extended-camera-control-properties"></a>Windows 8 拡張カメラコントロールのプロパティ

Windows 8 以降では、ユーザーモードクライアントでカメラのコントロール設定を取得または設定するために、次の追加のプロパティがサポートされています。

[**KSPROPERTY \_ CAMERACONTROL \_ FLASH \_ プロパティ**](ksproperty-cameracontrol-flash-property.md)

[**KSPROPERTY \_ CAMERACONTROL \_ IMAGE \_ PIN \_ 機能 \_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

[**関連する \_ \_ \_ プロパティの KSK \_ プロパティ CAMERACONTROL 領域 \_**](ksproperty-cameracontrol-region-of-interest-property.md)

[**KSPROPERTY \_ CAMERACONTROL \_ VIDEO \_ 安定化 \_ MODE \_ プロパティ**](ksproperty-cameracontrol-video-stabilization-mode-property.md)
