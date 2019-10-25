---
title: 拡張カメラ コントロールのプロパティ
ms.assetid: 27D94D73-D190-4C01-B082-7798CA71EDB4
description: 拡張カメラコントロールインターフェイスは、イメージのキャプチャ中にカメラの機能を制御するために使用されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63ce66ddc0ff3346f2788879129752804b203d5d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834404"
---
# <a name="extended-camera-control-properties"></a>拡張カメラ コントロールのプロパティ


Windows 8 以降で利用可能な拡張カメラコントロールインターフェイスは、イメージのキャプチャ中にカメラの機能を制御するために使用されます。 ドライバーは、次のカメラ機能を制御できます。

-   カメラのフラッシュ
-   イメージの pin とレコードの pin が相互に排他的であるかどうか
-   画像内の関心のある領域
-   ビデオ安定化

ドライバーは、カメラコントロール操作を非同期的に実行することもできます。つまり、1つ目の要求が完了するまで、操作に対するすべての要求が拒否されます。 ドライバーが非同期カメラコントロール操作を正常に実行した場合は、 [**KSEVENTSETID\_CameraAsyncControl**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-cameraasynccontrol)イベントをトリガーする必要があります。 詳細については、「 [**Ksk プロパティ\_CAMERACONTROL\_S\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s_ex) 」を参照してください。

UWP アプリはこれらのプロパティにアクセスして、カメラを構成できます。

## <a name="properties"></a>[プロパティ]


<a href="" id="ksproperty-cameracontrol-flash-property"></a>[**KSK プロパティ\_CAMERACONTROL\_FLASH\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-flash-property)  
カメラのフラッシュをオンまたはオフにする場合、またはフラッシュを自動モードにする場合に使用します。

<a href="" id="ksproperty-cameracontrol-image-pin-capability-property"></a>[**KSK プロパティ\_CAMERACONTROL\_IMAGE\_PIN\_機能\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-image-pin-capability-property)  
カメラのイメージの pin とレコードの pin が相互に排他的であるかどうかを識別するために使用されます。

<a href="" id="ksproperty-cameracontrol-region-of-interest-property"></a>[**KSK プロパティ\_CAMERACONTROL\_REGION\_\_関心のある\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-region-of-interest-property)  
カメラの対象領域の特性を取得または設定するために使用されます。

<a href="" id="ksproperty-cameracontrol-video-stabilization-mode-property"></a>[**KSPROPERTY\_CAMERACONTROL\_VIDEO\_安定化\_MODE\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-video-stabilization-mode-property)  
カメラのビデオ安定化特性を取得または設定するために使用します。

次のプロパティは、Windows 8.1 から使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE</strong></a></p></td>
<td><p>カメラの通常の静止モードまたはフォトシーケンスモードを取得または設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photoframerate"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE</strong></a></p></td>
<td><p>カメラの写真モードがシーケンスモードの場合に、現在の写真キャプチャフレームレートを取得するために使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomaxframerate"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE</strong></a></p></td>
<td><p>カメラがフォトシーケンスモードの場合に、キャプチャフレームの最大レートを取得または設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-phototriggertime"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME</strong></a></p></td>
<td><p>カメラドライバーのトリガー時間を取得または設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-warmstart"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART</strong></a></p></td>
<td><p>ウォームスタート (カメラ準備完了) 状態を取得または設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-maxvidfps-photores"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES</strong></a></p></td>
<td><p>特定の解像度でビデオキャプチャピンで可能なフレームレートの最大値を取得または設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photothumbnail"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL</strong></a></p></td>
<td><p>カメラのサムネイル機能を取得または設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-scenemode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE</strong></a></p></td>
<td><p>事前設定されたコントロールのコレクションを表すドライバー定義モードを取得または設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-torchmode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE</strong></a></p></td>
<td><p>カメラのフラッシュが低負荷の状態で使用されるメソッドを取得または設定するために使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-flashmode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE</strong></a></p></td>
<td><p>カメラの標準モードとシーケンス写真モードの両方について、フラッシュモード操作を取得または設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-optimizationhint"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT</strong></a></p></td>
<td><p>ホワイトバランスまたは手動温度値のどちらに対しても自動処理が行われるかどうかを取得または設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-whitebalancemode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE</strong></a></p></td>
<td><p>カメラが写真またはビデオ操作用に最適化されているかどうかを取得または設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-exposuremode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE</strong></a></p></td>
<td><p>自動処理が公開に対して行われるか、または手動の時刻値が使用されるかを取得または設定するために使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-focusmode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE</strong></a></p></td>
<td><p>カメラの自動、手動、およびプリセットのフォーカスモードを取得または設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-iso"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_ISO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_ISO</strong></a></p></td>
<td><p>カメラの ISO の事前設定または自動設定を取得または設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-fieldofview"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW</strong></a></p></td>
<td><p>カメラの位置のビューとピッチ角度のフィールドを取得するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-evcompensation"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION</strong></a></p></td>
<td><p>露出コントロールの調整設定を取得または設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-cameraangleoffset"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET</strong></a></p></td>
<td><p>カメラの位置のピッチとヨーの角度を取得するために使用します。</p></td>
</tr>
</tbody>
</table>

 

これらの構造体と列挙体は、拡張カメラコントロールインターフェイスをサポートしています。

## <a name="structures"></a>構造体


-   [**KSPROPERTY\_CAMERACONTROL\_S\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s_ex)
-   [**KSK プロパティ\_CAMERACONTROL\_FLASH\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_flash_s)
-   [**KSK プロパティ\_CAMERACONTROL\_IMAGE\_PIN\_機能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)
-   [**KSPROPERTY\_CAMERACONTROL\_REGION\_\_関心のある\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s)
-   [**KSPROPERTY\_CAMERACONTROL\_VIDEOSTABILIZATION\_モード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_videostabilization_mode_s)
-   [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOの設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)

## <a name="enumerations"></a>列挙


-   [**KS\_CameraControlAsyncOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ks_cameracontrolasyncoperation)
-   [**KSEVENT\_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksevent_cameracontrol)
-   [**KSK プロパティ\_CAMERACONTROL\_FLASH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_flash)
-   [**KSK プロパティ\_CAMERACONTROL\_IMAGE\_PIN\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_image_pin_capability)
-   [**KSK プロパティ\_CAMERACONTROL\_REGION\_関心のある\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_region_of_interest)
-   [**KSPROPERTY\_CAMERACONTROL\_VIDEO\_安定化\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_cameracontrol_video_stabilization_mode)

このインターフェイスを実装するドライバーコードの例は、「[拡張カメラコントロールのプロパティを実装する方法](how-to-implement-extended-camera-control-properties.md)」で説明されています。

 

 




