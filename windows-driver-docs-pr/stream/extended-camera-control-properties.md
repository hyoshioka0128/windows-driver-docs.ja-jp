---
title: 拡張のカメラ コントロールのプロパティ
ms.assetid: 27D94D73-D190-4C01-B082-7798CA71EDB4
description: 拡張のカメラのコントロール インターフェイスは、イメージ キャプチャ中にカメラの機能の制御に使用されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ed19dacfca630a12f51bb8b3e7d974c1b27ba23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560101"
---
# <a name="extended-camera-control-properties"></a>拡張のカメラ コントロールのプロパティ


以降、Windows 8 で利用可能な拡張のカメラのコントロール インターフェイスは、イメージ キャプチャ中にカメラの機能の制御に使用されます。 ドライバーは、これらのカメラ機能を制御できます。

-   カメラのフラッシュ
-   イメージの暗証番号 (pin) とレコードの pin が相互に排他的ながかどうか
-   イメージの関心領域
-   ビデオ安定化

ドライバーこともできますカメラ コントロールの操作を非同期的に実行する最初の要求が完了するまで、操作のすべての要求が拒否されたことを意味します。 ドライバーでは、非同期のカメラ コントロールの操作が正常に実行の場合はトリガーする、 [ **KSEVENTSETID\_CameraAsyncControl** ](https://msdn.microsoft.com/library/windows/hardware/jj714740)イベント。 参照してください[ **KSPROPERTY\_CAMERACONTROL\_S\_EX** ](https://msdn.microsoft.com/library/windows/hardware/jj151593)詳細についてはします。

UWP アプリは、カメラを構成するこれらのプロパティにアクセスできます。

## <a name="properties"></a>プロパティ


<a href="" id="ksproperty-cameracontrol-flash-property"></a>[**KSPROPERTY\_CAMERACONTROL\_FLASH\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj156041)  
オンまたはオフ、カメラのフラッシュを有効にする、または flash を自動モードにするために使用します。

<a href="" id="ksproperty-cameracontrol-image-pin-capability-property"></a>[**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj553706)  
カメラのイメージの暗証番号 (pin) とレコードの暗証番号 (pin) は相互に排他的であるかどうかを識別するために使用されます。

<a href="" id="ksproperty-cameracontrol-region-of-interest-property"></a>[**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj156042)  
取得または関心のあるカメラのリージョンの特性を設定するために使用します。

<a href="" id="ksproperty-cameracontrol-video-stabilization-mode-property"></a>[**KSPROPERTY\_CAMERACONTROL\_ビデオ\_安定化\_モード\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj156043)  
取得またはカメラのビデオ安定化の特性を設定するために使用します。

次のプロパティは、Windows 8.1 以降から使用できます。

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
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomode"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567582" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567582)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMODE</strong></a></p></td>
<td><p>取得またはカメラの標準静止画または写真シーケンス モードを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photoframerate"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567580" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567580)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOFRAMERATE</strong></a></p></td>
<td><p>カメラの写真のモードは、シーケンス モードのときに、写真のキャプチャの現在のフレーム レートを取得するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photomaxframerate"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567581" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567581)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOMAXFRAMERATE</strong></a></p></td>
<td><p>取得または写真シーケンス モードにあるときに、カメラの最大のキャプチャのフレーム レートを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-phototriggertime"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567584" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567584)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME</strong></a></p></td>
<td><p>取得またはカメラ ドライバーのトリガーの時刻を設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-warmstart"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567587" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567587)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WARMSTART</strong></a></p></td>
<td><p>取得またはウォーム スタート (カメラの準備完了) 状態を設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-maxvidfps-photores"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567578" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567578)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_MAXVIDFPS_PHOTORES</strong></a></p></td>
<td><p>取得または特定の解像度でビデオ キャプチャ ピンの可能な最大の可能なフレーム レートを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-photothumbnail"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567583" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567583)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTHUMBNAIL</strong></a></p></td>
<td><p>カメラのサムネイルの機能の設定を取得または使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-scenemode"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567585" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567585)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_SCENEMODE</strong></a></p></td>
<td><p>取得または事前設定されたコントロールのコレクションを表すドライバーが定義されているモードを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-torchmode"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567586" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567586)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_TORCHMODE</strong></a></p></td>
<td><p>取得または低光状態でカメラのフラッシュを使用する方法を設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-flashmode"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567575" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567575)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FLASHMODE</strong></a></p></td>
<td><p>取得またはフラッシュのモードで両方の通常の操作とカメラのシーケンスの写真のモードを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-optimizationhint"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567579" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567579)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_OPTIMIZATIONHINT</strong></a></p></td>
<td><p>取得またはホワイト バランスまたは手動の温度の値の自動処理が発生するかどうかを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-whitebalancemode"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567588" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567588)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_WHITEBALANCEMODE</strong></a></p></td>
<td><p>取得またはカメラが写真やビデオの操作の最適化されたかどうかを設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-exposuremode"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567573" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567573)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EXPOSUREMODE</strong></a></p></td>
<td><p>取得または危険度の自動処理が行われますか、手動のタイム値が使用するかどうかを設定するために使用します。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-focusmode"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567576" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567576)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSMODE</strong></a></p></td>
<td><p>取得または自動、手動で設定し、カメラのフォーカス モードを事前設定するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-iso"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567577" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_ISO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567577)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_ISO</strong></a></p></td>
<td><p>カメラの事前設定または自動の ISO 設定の設定を取得または使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-fieldofview"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567574" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567574)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_FIELDOFVIEW</strong></a></p></td>
<td><p>ビューのフィールドを取得し、カメラの位置の角度を登板するために使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="ksproperty-cameracontrol-extended-evcompensation"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567572" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567572)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_EVCOMPENSATION</strong></a></p></td>
<td><p>取得またはコントロールの露出の調整設定を設定する場合に使用されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="ksproperty-cameracontrol-extended-cameraangleoffset"></a><a href="https://msdn.microsoft.com/library/windows/hardware/dn567571" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn567571)"><strong>KSPROPERTY_CAMERACONTROL_EXTENDED_CAMERAANGLEOFFSET</strong></a></p></td>
<td><p>ピッチを取得し、カメラの位置の角度のヨーするために使用します。</p></td>
</tr>
</tbody>
</table>

 

これらの構造および列挙体は、拡張のカメラ コントロールのインターフェイスをサポートします。

## <a name="structures"></a>構造体


-   [**KSPROPERTY\_CAMERACONTROL\_S\_例**](https://msdn.microsoft.com/library/windows/hardware/jj151593)
-   [**KSPROPERTY\_CAMERACONTROL\_FLASH\_S**](https://msdn.microsoft.com/library/windows/hardware/jj151590)
-   [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_S**](https://msdn.microsoft.com/library/windows/hardware/jj553707)
-   [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_S**](https://msdn.microsoft.com/library/windows/hardware/jj151592)
-   [**KSPROPERTY\_CAMERACONTROL\_VIDEOSTABILIZATION\_モード\_S**](https://msdn.microsoft.com/library/windows/hardware/jj151594)
-   [**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)
-   [**KSCAMERA\_EXTENDEDPROP\_値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)
-   [**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)
-   [**KSCAMERA\_MAXVIDEOFPS\_FORPHOTORES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_maxvideofps_forphotores)
-   [**KSCAMERA\_EXTENDEDPROP\_VIDEOPROCSETTING**](https://msdn.microsoft.com/library/windows/hardware/dn567566)
-   [**KSCAMERA\_EXTENDEDPROP\_FIELDOFVIEW**](https://msdn.microsoft.com/library/windows/hardware/dn567562)

## <a name="enumerations"></a>列挙


-   [**KS\_CameraControlAsyncOperation**](https://msdn.microsoft.com/library/windows/hardware/jj151596)
-   [**KSEVENT\_CAMERACONTROL**](https://msdn.microsoft.com/library/windows/hardware/jj151587)
-   [**KSPROPERTY\_CAMERACONTROL\_フラッシュ**](https://msdn.microsoft.com/library/windows/hardware/jj151589)
-   [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能**](https://msdn.microsoft.com/library/windows/hardware/jj553705)
-   [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_対象**](https://msdn.microsoft.com/library/windows/hardware/jj151591)
-   [**KSPROPERTY\_CAMERACONTROL\_ビデオ\_安定化\_モード**](https://msdn.microsoft.com/library/windows/hardware/jj151595)

このインターフェイスを実装するドライバー コードの例が記載[方法を実装拡張カメラ コントロール プロパティ](how-to-implement-extended-camera-control-properties.md)します。

 

 




