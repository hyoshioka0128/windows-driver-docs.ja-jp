---
title: カメラ コントロールのプロパティ
description: カメラ コントロールのプロパティ
ms.assetid: 36a57245-e89e-4418-b0c4-a4c1479413b2
keywords:
- カメラ コントロール プロパティ WDK ビデオのキャプチャします。
- コントロールのプロパティの WDK ビデオ キャプチャ
- PROPSETID_VIDCAP_CAMERACONTROL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f1de07d7f9e7aa29fbbd069823523fede34c63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386673"
---
# <a name="camera-control-properties"></a>カメラ コントロールのプロパティ


[PROPSETID\_しました\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)ビデオ_カメラの制御に関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_しました\_CAMERACONTROL プロパティ セット。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>PROPSETID_VIDCAP_CAMERACONTROL KS プロパティ</th>
<th>プロパティの説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXPOSURE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure)"><strong>KSPROPERTY_CAMERACONTROL_EXPOSURE</strong></a></p></td>
<td><p>カメラのデジタル公開期間を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCUS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus)"><strong>KSPROPERTY_CAMERACONTROL_FOCUS</strong></a></p></td>
<td><p>カメラのフォーカスの設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IRIS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris)"><strong>KSPROPERTY_CAMERACONTROL_IRIS</strong></a></p></td>
<td><p>カメラの絞り設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ZOOM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom)"><strong>KSPROPERTY_CAMERACONTROL_ZOOM</strong></a></p></td>
<td><p>カメラのズーム設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PAN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan)"><strong>KSPROPERTY_CAMERACONTROL_PAN</strong></a></p></td>
<td><p>カメラのコントロールはパン設定です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ROLL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll)"><strong>KSPROPERTY_CAMERACONTROL_ROLL</strong></a></p></td>
<td><p>カメラのコントロールは、設定をロールバックします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_TILT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt)"><strong>KSPROPERTY_CAMERACONTROL_TILT</strong></a></p></td>
<td><p>カメラのコントロールは、設定を傾けます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-scanmode" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_SCANMODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-scanmode)"><strong>KSPROPERTY_CAMERACONTROL_SCANMODE</strong></a></p></td>
<td><p>インターリーブ、または非インターリーブドなどのカメラのセンサーのスキャン モードを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-privacy" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PRIVACY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-privacy)"><strong>KSPROPERTY_CAMERACONTROL_PRIVACY</strong></a></p></td>
<td><p>カメラ センサーが、ビデオをキャプチャする必要がありますか、ビデオのキャプチャが妨げがかどうかを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PANTILT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt)"><strong>KSPROPERTY_CAMERACONTROL_PANTILT</strong></a></p></td>
<td><p>カメラの絶対パンおよび傾きの設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PAN_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pan-relative)"><strong>KSPROPERTY_CAMERACONTROL_PAN_RELATIVE</strong></a></p></td>
<td><p>現在の値から垂直軸の周りのカメラの相対的な回転を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_TILT_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-tilt-relative)"><strong>KSPROPERTY_CAMERACONTROL_TILT_RELATIVE</strong></a></p></td>
<td><p>現在の位置から水平軸の周りでカメラの相対的な回転を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-roll-relative)"><strong>KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE</strong></a></p></td>
<td><p>現在の値からの軸を表示するイメージに関するカメラの相対的な回転を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-zoom-relative)"><strong>KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE</strong></a></p></td>
<td><p>カメラの相対的なズームが現在の値から設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-exposure-relative)"><strong>KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE</strong></a></p></td>
<td><p>現在の値からのカメラの相対的なシャッター スピードを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-iris-relative)"><strong>KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE</strong></a></p></td>
<td><p>現在の値からのカメラの相対 aperture 設定を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focus-relative)"><strong>KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE</strong></a></p></td>
<td><p>カメラの相対的なフォーカスを現在の値から設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt-relative" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-pantilt-relative)"><strong>KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE</strong></a></p></td>
<td><p>カメラの相対的なパンとその現在の値の設定の傾きを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focal-length" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-focal-length)"><strong>KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH</strong></a></p></td>
<td><p>カメラの焦点距離を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-auto-exposure-priority" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-auto-exposure-priority)"><strong>KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY</strong></a></p></td>
<td><p>デバイスでフレーム レートを動的に変更できるかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows8-extended-camera-control-properties"></a>Windows 8 がカメラ コントロールのプロパティを拡張


Windows 8 以降、これらの追加プロパティはサポートされてユーザー モードのクライアントを取得またはカメラのコントロールの設定を設定します。 詳細については、次を参照してください。[カメラ コントロールのプロパティの拡張](extended-camera-control-properties.md)と[方法を実装拡張カメラ コントロール プロパティ](how-to-implement-extended-camera-control-properties.md)します。

| PROPSETID\_しました\_CAMERACONTROL KS プロパティ                                                                                           | プロパティの説明                                                                                                  |
|------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| [**KSPROPERTY\_CAMERACONTROL\_FLASH\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-flash-property)                                         | ユーザー モードのクライアントでは、必要に応じてこのプロパティを使用して取得またはカメラのフラッシュのコントロールの特性を設定します。                |
| [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-image-pin-capability-property)         | ユーザー モードのクライアントでは、このプロパティを使用して、カメラのイメージの暗証番号 (pin) とレコードの暗証番号 (pin) は相互に排他的であるかどうかを識別します。 |
| [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-region-of-interest-property)             | 必要に応じて、ユーザー モード クライアントは、目的の特徴のカメラのリージョンの設定を取得またはこのプロパティを使用します。           |
| [**KSPROPERTY\_CAMERACONTROL\_ビデオ\_安定化\_モード\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-video-stabilization-mode-property) | ユーザー モードのクライアントでは、必要に応じてこのプロパティを使用して取得またはカメラのビデオ安定化の特性を設定します。          |

 

## <a href="" id="win8-1-extended-props"></a>Windows 8.1 の拡張のカメラ コントロールのプロパティ


Windows 8.1 では、以降、 [KSPROPERTYSETID\_ExtendedCameraControl](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropertysetid-extendedcameracontrol)プロパティ セットは、カメラの写真のシーケンス処理の他のコントロールを提供します。 これらのコントロールを実装する方法の詳細については、これらのトピックを参照してください。

-   [拡張のカメラ コントロールのプロパティ](extended-camera-control-properties.md)
-   [拡張のカメラ コントロールのプロパティを実装するには、方法](how-to-implement-extended-camera-control-properties.md)
-   [拡張のカメラ コントロール ペイロード](extended-camera-control-payloads.md)
-   [写真シーケンス モード](photo-sequence-mode.md)

 

 




