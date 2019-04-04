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
ms.openlocfilehash: 2b658830552bfc68f31da8d31c624072257a1f51
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350079"
---
# <a name="camera-control-properties"></a>カメラ コントロールのプロパティ


[PROPSETID\_しました\_CAMERACONTROL](https://msdn.microsoft.com/library/windows/hardware/ff567802)ビデオ_カメラの制御に関連するプロパティがプロパティ セットに含まれています。 次の表に、プロパティ、PROPSETID の一部である\_しました\_CAMERACONTROL プロパティ セット。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564401" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXPOSURE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564401)"><strong>KSPROPERTY_CAMERACONTROL_EXPOSURE</strong></a></p></td>
<td><p>カメラのデジタル公開期間を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564410" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564410)"><strong>KSPROPERTY_CAMERACONTROL_FOCUS</strong></a></p></td>
<td><p>カメラのフォーカスの設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564415" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IRIS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564415)"><strong>KSPROPERTY_CAMERACONTROL_IRIS</strong></a></p></td>
<td><p>カメラの絞り設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564459" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ZOOM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564459)"><strong>KSPROPERTY_CAMERACONTROL_ZOOM</strong></a></p></td>
<td><p>カメラのズーム設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564424" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PAN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564424)"><strong>KSPROPERTY_CAMERACONTROL_PAN</strong></a></p></td>
<td><p>カメラのコントロールはパン設定です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564432" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ROLL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564432)"><strong>KSPROPERTY_CAMERACONTROL_ROLL</strong></a></p></td>
<td><p>カメラのコントロールは、設定をロールバックします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564454" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_TILT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564454)"><strong>KSPROPERTY_CAMERACONTROL_TILT</strong></a></p></td>
<td><p>カメラのコントロールは、設定を傾けます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564452" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_SCANMODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564452)"><strong>KSPROPERTY_CAMERACONTROL_SCANMODE</strong></a></p></td>
<td><p>インターリーブ、または非インターリーブドなどのカメラのセンサーのスキャン モードを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564430" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PRIVACY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564430)"><strong>KSPROPERTY_CAMERACONTROL_PRIVACY</strong></a></p></td>
<td><p>カメラ センサーが、ビデオをキャプチャする必要がありますか、ビデオのキャプチャが妨げがかどうかを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564425" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PANTILT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564425)"><strong>KSPROPERTY_CAMERACONTROL_PANTILT</strong></a></p></td>
<td><p>カメラの絶対パンおよび傾きの設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564429" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PAN_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564429)"><strong>KSPROPERTY_CAMERACONTROL_PAN_RELATIVE</strong></a></p></td>
<td><p>現在の値から垂直軸の周りのカメラの相対的な回転を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564456" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_TILT_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564456)"><strong>KSPROPERTY_CAMERACONTROL_TILT_RELATIVE</strong></a></p></td>
<td><p>現在の位置から水平軸の周りでカメラの相対的な回転を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564435" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564435)"><strong>KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE</strong></a></p></td>
<td><p>現在の値からの軸を表示するイメージに関するカメラの相対的な回転を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564460" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564460)"><strong>KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE</strong></a></p></td>
<td><p>カメラの相対的なズームが現在の値から設定を制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564404" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564404)"><strong>KSPROPERTY_CAMERACONTROL_EXPOSURE_RELATIVE</strong></a></p></td>
<td><p>現在の値からのカメラの相対的なシャッター スピードを制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564417" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564417)"><strong>KSPROPERTY_CAMERACONTROL_IRIS_RELATIVE</strong></a></p></td>
<td><p>現在の値からのカメラの相対 aperture 設定を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564413" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564413)"><strong>KSPROPERTY_CAMERACONTROL_FOCUS_RELATIVE</strong></a></p></td>
<td><p>カメラの相対的なフォーカスを現在の値から設定を制御します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564427" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564427)"><strong>KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE</strong></a></p></td>
<td><p>カメラの相対的なパンとその現在の値の設定の傾きを制御します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564406" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564406)"><strong>KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH</strong></a></p></td>
<td><p>カメラの焦点距離を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564399" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564399)"><strong>KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY</strong></a></p></td>
<td><p>デバイスでフレーム レートを動的に変更できるかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows8-extended-camera-control-properties"></a>Windows 8 がカメラ コントロールのプロパティを拡張


Windows 8 以降、これらの追加プロパティはサポートされてユーザー モードのクライアントを取得またはカメラのコントロールの設定を設定します。 詳細については、[カメラ コントロールのプロパティの拡張](extended-camera-control-properties.md)と[方法を実装拡張カメラ コントロール プロパティ](how-to-implement-extended-camera-control-properties.md)を参照してください。

| PROPSETID\_しました\_CAMERACONTROL KS プロパティ                                                                                           | プロパティの説明                                                                                                  |
|------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| [**KSPROPERTY\_CAMERACONTROL\_FLASH\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj156041)                                         | ユーザー モードのクライアントでは、必要に応じてこのプロパティを使用して取得またはカメラのフラッシュのコントロールの特性を設定します。                |
| [**KSPROPERTY\_CAMERACONTROL\_イメージ\_PIN\_機能\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj553706)         | ユーザー モードのクライアントでは、このプロパティを使用して、カメラのイメージの暗証番号 (pin) とレコードの暗証番号 (pin) は相互に排他的であるかどうかを識別します。 |
| [**KSPROPERTY\_CAMERACONTROL\_リージョン\_の\_関心\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj156042)             | 必要に応じて、ユーザー モード クライアントは、目的の特徴のカメラのリージョンの設定を取得またはこのプロパティを使用します。           |
| [**KSPROPERTY\_CAMERACONTROL\_ビデオ\_安定化\_モード\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/jj156043) | ユーザー モードのクライアントでは、必要に応じてこのプロパティを使用して取得またはカメラのビデオ安定化の特性を設定します。          |

 

## <a href="" id="win8-1-extended-props"></a>Windows 8.1 の拡張のカメラ コントロールのプロパティ


Windows 8.1 では、以降、 [KSPROPERTYSETID\_ExtendedCameraControl](https://msdn.microsoft.com/library/windows/hardware/dn567570)プロパティ セットは、カメラの写真のシーケンス処理の他のコントロールを提供します。 これらのコントロールを実装する方法の詳細については、これらのトピックを参照してください。

-   [拡張のカメラ コントロールのプロパティ](extended-camera-control-properties.md)
-   [拡張のカメラ コントロールのプロパティを実装するには、方法](how-to-implement-extended-camera-control-properties.md)
-   [拡張のカメラ コントロール ペイロード](extended-camera-control-payloads.md)
-   [写真シーケンス モード](photo-sequence-mode.md)

 

 




