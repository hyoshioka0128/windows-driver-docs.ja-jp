---
title: Windows 8.1 用の新しい AVStream インターフェイス
description: AVStream ストリーミング メディア ドライバー インターフェイスは、Windows 8.1 以降、新しいカメラ プラットフォームの機能をサポートするために拡張されます。
ms.assetid: 1D06A754-236B-441D-A0BB-A78B419270E9
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5757cf789163b01866878740c822b69456b8012f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376096"
---
# <a name="new-avstream-interfaces-for-windows-81"></a>Windows 8.1 用の新しい AVStream インターフェイス


AVStream ストリーミング メディア ドライバー インターフェイスは、Windows 8.1 以降、新しいカメラ プラットフォームの機能をサポートするために拡張されます。

## <a name="camera-platform"></a>カメラのプラットフォーム


カメラ コントロールを拡張するには、Windows 8.1 以降します。 これらのカメラ コントロールを実装する方法については、下にあるトピックを参照してください。[カメラ コントロール プロパティ](camera-control-properties.md)します。

これらのデバイス ドライバー インターフェイス (Ddi) は、これらの拡張機能をサポートし、新規または更新。

-   [**KSCAMERA\_EXTENDEDPROP\_CAMERAOFFSET**](https://msdn.microsoft.com/library/windows/hardware/dn567560)
-   [**KSCAMERA\_EXTENDEDPROP\_EVCOMPENSATION**](https://msdn.microsoft.com/library/windows/hardware/dn567561)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://msdn.microsoft.com/library/windows/hardware/dn567562)
-   [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://msdn.microsoft.com/library/windows/hardware/dn567566)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [KSEVENTSETID\_VolumeLimit](https://msdn.microsoft.com/library/windows/hardware/dn567568)
-   [**KSEVENT\_VOLUMELIMIT\_CHANGED**](https://msdn.microsoft.com/library/windows/hardware/dn567569)
-   [KSPROPERTYSETID\_ExtendedCameraControl](https://msdn.microsoft.com/library/windows/hardware/dn567570) (これらのプロパティが含まれています)。
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_CAMERAANGLEOFFSET**](https://msdn.microsoft.com/library/windows/hardware/dn567571)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_EVCOMPENSATION**](https://msdn.microsoft.com/library/windows/hardware/dn567572)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_EXPOSUREMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567573)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_FIELDOFVIEW**](https://msdn.microsoft.com/library/windows/hardware/dn567574)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_FLASHMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567575)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567576)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_ISO**](https://msdn.microsoft.com/library/windows/hardware/dn567577)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_MAXVIDFPS\_PHOTORES**](https://msdn.microsoft.com/library/windows/hardware/dn567578)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_OPTIMIZATIONHINT**](https://msdn.microsoft.com/library/windows/hardware/dn567579)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOFRAMERATE**](https://msdn.microsoft.com/library/windows/hardware/dn567580)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMAXFRAMERATE**](https://msdn.microsoft.com/library/windows/hardware/dn567581)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567582)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTHUMBNAIL**](https://msdn.microsoft.com/library/windows/hardware/dn567583)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_PHOTOTRIGGERTIME**](https://msdn.microsoft.com/library/windows/hardware/dn567584)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_SCENEMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567585)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_TORCHMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567586)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_WARMSTART という**](https://msdn.microsoft.com/library/windows/hardware/dn567587)
    -   [**KSPROPERTY\_CAMERACONTROL\_拡張\_WHITEBALANCEMODE**](https://msdn.microsoft.com/library/windows/hardware/dn567588)
-   [**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](https://msdn.microsoft.com/library/windows/hardware/dn567589)
-   [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_S** ](https://msdn.microsoft.com/library/windows/hardware/jj553707) (新しい**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_シーケンス\_排他\_WITH\_レコード**メンバー)
-   [**KSP\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff566722) (新しい**フラグ**メンバー)
-   [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_S** ](https://msdn.microsoft.com/library/windows/hardware/jj151592) (新しい**構成**メンバー)
-   [**KS\_VideoControlFlags** ](https://msdn.microsoft.com/library/windows/hardware/ff567696) (新しい**KS\_VideoControlFlag\_StartPhotoSequenceCapture**と**KS\_VideoControlFlag\_StopPhotoSequenceCapture**定数値)
-   [**KS\_FRAME\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567645) (new **FrameCompletionNumber** member)
-   メモも追加[KSPROPERTYSETID\_ExtendedCameraControl](https://msdn.microsoft.com/library/windows/hardware/dn567570)プロパティ設定で表示されている[ビデオ キャプチャ ミニドライバー プロパティ セット](https://msdn.microsoft.com/library/windows/hardware/ff568714)します。

 

 




