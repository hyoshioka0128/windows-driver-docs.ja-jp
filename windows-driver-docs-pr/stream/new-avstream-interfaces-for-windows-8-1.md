---
title: Windows 8.1 用の新しい AVStream インターフェイス
description: AVStream ストリーミング メディア ドライバー インターフェイスは、Windows 8.1 以降、新しいカメラ プラットフォームの機能をサポートするために拡張されます。
ms.assetid: 1D06A754-236B-441D-A0BB-A78B419270E9
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: a993e9c969075cf6d771bd7f5ad410d80ba1942f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363275"
---
# <a name="new-avstream-interfaces-for-windows-81"></a>Windows 8.1 用の新しい AVStream インターフェイス


AVStream ストリーミング メディア ドライバー インターフェイスは、Windows 8.1 以降、新しいカメラ プラットフォームの機能をサポートするために拡張されます。

## <a name="camera-platform"></a>カメラのプラットフォーム


カメラ コントロールを拡張するには、Windows 8.1 以降します。 これらのカメラ コントロールを実装する方法については、下にあるトピックを参照してください。[カメラ コントロール プロパティ](camera-control-properties.md)します。

これらのデバイス ドライバー インターフェイス (Ddi) は、これらの拡張機能をサポートし、新規または更新。

-   [**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_cameraoffset)
-   [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_evcompensation)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)
-   [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [KSEVENTSETID\_VolumeLimit](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-volumelimit)
-   [**KSEVENT\_VOLUMELIMIT\_CHANGED**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-volumelimit-changed)
-   [KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol) (これらのプロパティが含まれています)。
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_CAMERAANGLEOFFSET**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_EVCOMPENSATION**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_EXPOSUREMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_ISO**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_MAXVIDFPS\_PHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTRIGGERTIME**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_TORCHMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_WARMSTART という**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_WHITEBALANCEMODE**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode)
-   [**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-proposedataformat2)
-   [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s) (新しい**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_シーケンス\_排他\_WITH\_レコード**メンバー)
-   [**KSP\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin) (新しい**フラグ**メンバー)
-   [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s) (新しい**構成**メンバー)
-   [**KS\_VideoControlFlags** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ks_videocontrolflags) (新しい**KS\_VideoControlFlag\_StartPhotoSequenceCapture**と**KS\_VideoControlFlag\_StopPhotoSequenceCapture**定数値)
-   [**KS\_FRAME\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info) (new **FrameCompletionNumber** member)
-   メモも追加[KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)プロパティ設定で表示されている[ビデオ キャプチャ ミニドライバー プロパティ セット](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-minidriver-property-sets)します。

 

 




