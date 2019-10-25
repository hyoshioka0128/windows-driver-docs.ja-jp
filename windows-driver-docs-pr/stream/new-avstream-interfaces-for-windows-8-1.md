---
title: Windows 8.1 用の新しい AVStream インターフェイス
description: AVStream streaming media driver インターフェイスは、Windows 8.1 から始まる新しいカメラプラットフォーム機能をサポートするように拡張されています。
ms.assetid: 1D06A754-236B-441D-A0BB-A78B419270E9
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: e5feb7427274586d850a539a22f41ca5551ff450
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823594"
---
# <a name="new-avstream-interfaces-for-windows-81"></a>Windows 8.1 用の新しい AVStream インターフェイス


AVStream streaming media driver インターフェイスは、Windows 8.1 から始まる新しいカメラプラットフォーム機能をサポートするように拡張されています。

## <a name="camera-platform"></a>カメラのプラットフォーム


カメラコントロールは Windows 8.1 から拡張されます。 これらのカメラコントロールを実装する方法の詳細については、「[カメラコントロールのプロパティ](camera-control-properties.md)」のトピックを参照してください。

これらのデバイスドライバーインターフェイス (DDIs) は、これらの拡張機能をサポートし、新しいまたは更新されています。

-   [**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)
-   [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)
-   [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOの設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [KSEVENTSETID\_VolumeLimit](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-volumelimit)
-   [**KSEVENT\_VOLUMELIMIT\_変更されました**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-volumelimit-changed)
-   [Ksk Propertysetid\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol) (これらのプロパティを含む)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_CAMERAANGLEOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_EXPOSUREMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FLASHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_FOCUSMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_ISO**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_MAXVIDFPS\_PHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_OPTIMIZATIONHINT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint)
    -   [**KSK プロパティ\_CAMERACONTROL\_拡張\_PHOTOFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate)
    -   [**KSK プロパティ\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)
    -   [**KSK プロパティ\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_PHOTOTRIGGERTIME**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_SCENEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_TORCHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_の起動**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart)
    -   [**KSK プロパティ\_CAMERACONTROL\_EXTENDED\_WHITEBALANCEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode)
-   [**KSK プロパティ\_PIN\_PROPOSEDATAFORMAT2**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat2)
-   [**Ksk プロパティ\_CAMERACONTROL\_image\_pin\_機能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s) (新しい**KSK プロパティ\_CAMERACONTROL\_IMAGE\_ピン\_機能\_SEQUENCE\_EXCLUSIVE @no__\_レコードメンバーを含む t_14_** )
-   [**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin) (新しい**フラグ**メンバー)
-   [**Ksk プロパティ\_CAMERACONTROL\_REGION\_\_関心のある\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s) (新しい**構成**メンバー)
-   [**Ks\_VideoControlFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_videocontrolflags) (new **KS\_videocontrolflags\_StartPhotoSequenceCapture**および**KS\_videocontrolflags\_StopPhotoSequenceCapture**定数値)
-   [**KS\_FRAME\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info) (new **FrameCompletionNumber** member)
-   また、「 [Video Capture ミニドライバープロパティセット](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-minidriver-property-sets)」に記載されている追加の[ksk Propertysetid\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)プロパティセットにも注意してください。

 

 




