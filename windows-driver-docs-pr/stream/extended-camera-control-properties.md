---
title: 拡張カメラ コントロールのプロパティ
ms.assetid: 27D94D73-D190-4C01-B082-7798CA71EDB4
description: 拡張のカメラのコントロール インターフェイスは、イメージ キャプチャ中にカメラの機能の制御に使用されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ece0bb0e87b86581407a8b5815cbddc8ae3593c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384111"
---
# <a name="extended-camera-control-properties"></a>拡張カメラ コントロールのプロパティ


以降、Windows 8 で利用可能な拡張のカメラのコントロール インターフェイスは、イメージ キャプチャ中にカメラの機能の制御に使用されます。 ドライバーは、これらのカメラ機能を制御できます。

-   カメラのフラッシュ
-   イメージの暗証番号 (pin) とレコードの pin が相互に排他的ながかどうか
-   イメージの関心領域
-   ビデオ安定化

ドライバーこともできますカメラ コントロールの操作を非同期的に実行する最初の要求が完了するまで、操作のすべての要求が拒否されたことを意味します。 ドライバーでは、非同期のカメラ コントロールの操作が正常に実行の場合はトリガーする、 [ **KSEVENTSETID\_CameraAsyncControl** ](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-cameraasynccontrol)イベント。 参照してください[ **KSPROPERTY\_CAMERACONTROL\_S\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s_ex)詳細についてはします。

UWP アプリは、カメラを構成するこれらのプロパティにアクセスできます。

## <a name="properties"></a>プロパティ


<a href="" id="ksproperty-cameracontrol-flash-property"></a>[**KSPROPERTY\_CAMERACONTROL\_FLASH\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-flash-property)  
オンまたはオフ、カメラのフラッシュを有効にする、または flash を自動モードにするために使用します。

<a href="" id="ksproperty-cameracontrol-image-pin-capability-property"></a>[**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-image-pin-capability-property)  
カメラのイメージの暗証番号 (pin) とレコードの暗証番号 (pin) は相互に排他的であるかどうかを識別するために使用されます。

<a href="" id="ksproperty-cameracontrol-region-of-interest-property"></a>[**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-region-of-interest-property)  
取得または関心のあるカメラのリージョンの特性を設定するために使用します。

<a href="" id="ksproperty-cameracontrol-video-stabilization-mode-property"></a>[**KSPROPERTY\_CAMERACONTROL\_ビデオ\_安定化\_モード\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-video-stabilization-mode-property)  
取得またはカメラのビデオ安定化の特性を設定するために使用します。

次のプロパティは、Windows 8.1 以降から使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>項目</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE</strong></a></p></td>
<td><p>取得またはカメラの標準静止画または写真シーケンス モードを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photoframerate"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoframerate)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE</strong></a></p></td>
<td><p>カメラの写真のモードは、シーケンス モードのときに、写真のキャプチャの現在のフレーム レートを取得するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomaxframerate"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomaxframerate)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE</strong></a></p></td>
<td><p>取得または写真シーケンス モードにあるときに、カメラの最大のキャプチャのフレーム レートを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-phototriggertime"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-phototriggertime)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME</strong></a></p></td>
<td><p>取得またはカメラ ドライバーのトリガーの時刻を設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-warmstart"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-warmstart)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART</strong></a></p></td>
<td><p>取得またはウォーム スタート (カメラの準備完了) 状態を設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-maxvidfps-photores"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-maxvidfps-photores)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES</strong></a></p></td>
<td><p>取得または特定の解像度でビデオ キャプチャ ピンの可能な最大の可能なフレーム レートを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photothumbnail"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photothumbnail)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL</strong></a></p></td>
<td><p>カメラのサムネイルの機能の設定を取得または使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-scenemode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE</strong></a></p></td>
<td><p>取得または事前設定されたコントロールのコレクションを表すドライバーが定義されているモードを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-torchmode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-torchmode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE</strong></a></p></td>
<td><p>取得または低光状態でカメラのフラッシュを使用する方法を設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-flashmode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE</strong></a></p></td>
<td><p>取得またはフラッシュのモードで両方の通常の操作とカメラのシーケンスの写真のモードを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-optimizationhint"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-optimizationhint)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT</strong></a></p></td>
<td><p>取得またはホワイト バランスまたは手動の温度の値の自動処理が発生するかどうかを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-whitebalancemode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-whitebalancemode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE</strong></a></p></td>
<td><p>取得またはカメラが写真やビデオの操作の最適化されたかどうかを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-exposuremode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-exposuremode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE</strong></a></p></td>
<td><p>取得または危険度の自動処理が行われますか、手動のタイム値が使用するかどうかを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-focusmode"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE</strong></a></p></td>
<td><p>取得または自動、手動で設定し、カメラのフォーカス モードを事前設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-iso"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_ISO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_ISO</strong></a></p></td>
<td><p>カメラの事前設定または自動の ISO 設定の設定を取得または使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-fieldofview"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-fieldofview)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW</strong></a></p></td>
<td><p>ビューのフィールドを取得し、カメラの位置の角度を登板するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-evcompensation"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-evcompensation)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION</strong></a></p></td>
<td><p>取得またはコントロールの露出の調整設定を設定する場合に使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-cameraangleoffset"></a><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-cameraangleoffset)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET</strong></a></p></td>
<td><p>ピッチを取得し、カメラの位置の角度のヨーするために使用します。</p></td>
</tr>
</tbody>
</table>

 

これらの構造および列挙体は、拡張のカメラ コントロールのインターフェイスをサポートします。

## <a name="structures"></a>構造体


-   [**KSPROPERTY\_CAMERACONTROL\_S\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s_ex)
-   [**KSPROPERTY\_CAMERACONTROL\_FLASH\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_flash_s)
-   [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)
-   [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_region_of_interest_s)
-   [**KSPROPERTY\_CAMERACONTROL\_VIDEOSTABILIZATION\_モード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_videostabilization_mode_s)
-   [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_fieldofview)

## <a name="enumerations"></a>列挙


-   [**KS\_CameraControlAsyncOperation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ks_cameracontrolasyncoperation)
-   [**KSEVENT\_CAMERACONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksevent_cameracontrol)
-   [**KSPROPERTY\_CAMERACONTROL\_フラッシュ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_flash)
-   [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_image_pin_capability)
-   [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_対象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_region_of_interest)
-   [**KSPROPERTY\_CAMERACONTROL\_ビデオ\_安定化\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_video_stabilization_mode)

このインターフェイスを実装するドライバー コードの例が記載[方法を実装拡張カメラ コントロール プロパティ](how-to-implement-extended-camera-control-properties.md)します。

 

 




