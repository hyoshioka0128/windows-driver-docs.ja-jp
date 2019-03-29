---
title: WIA\_IPA\_データ型
description: WIA\_IPA\_DATATYPE プロパティには、デバイスの設定の現在のデータ型が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: d86c06c2-1d37-4b82-832c-c468c1b4fc33
keywords:
- WIA_IPA_DATATYPE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_DATATYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0eeb0cb57cc80055d54c3a2a15ea93079aab8a41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574564"
---
# <a name="wiaipadatatype"></a>WIA\_IPA\_データ型


WIA\_IPA\_DATATYPE プロパティには、デバイスの設定の現在のデータ型が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_datatype_si"></span><span id="DDK_WIA_IPA_DATATYPE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

アプリケーションの読み取り、WIA\_IPA\_イメージのデータ型を決定するデータ型プロパティ。 アプリケーションでは、転送されるイメージの現在のデータ型を設定するには、このプロパティを書き込みます。

次の表に、WIA で有効な定数\_IPA\_データ型と、 [ **WIA\_IPA\_形式**](wia-ipa-format.md)プロパティが設定されていません。WiaImgFmt に\_RAW です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>データ型</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DATA_AUTO</p></td>
<td><p>この値は、フラット ベッドとフィーダーを含むすべてプログラミング可能なイメージ データ ソース アイテムに対して無効です。 この値が、WIA ミニ ドライバー、WIA アプリケーション クライアントによってサポートされている場合に設定できます。<strong>WIA_IPA_DATATYPE</strong>デバイスでの色の自動検出を有効にするためにします。</p>
<p>WIA_DATA_AUTO を設定すると、WIA ミニ ドライバーを更新する必要があります<a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a> WIA_DEPTH_AUTO (これは、デバイスは、自動の色をサポートしている場合は、サポートされている値をある必要があります) を同じ項目。</p>
<p>ときに、 <a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a> WIA_DEPTH_AUTO がサポートされる値、 <strong>WIA_IPA_DATATYPE</strong> WIA_DATA_AUTO の値が省略可能なされなくなり、必要な値になります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_COLOR</p></td>
<td><p>スキャン データは、赤、緑、青 (RGB) です。 完全な色形式は次の WIA プロパティを使用してについて説明します。</p>
<ul>
<li><p><a href="wia-ipa-channels-per-pixel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_CHANNELS_PER_PIXEL&lt;/strong&gt;](wia-ipa-channels-per-pixel.md)"><strong>WIA_IPA_CHANNELS_PER_PIXEL</strong></a></p></li>
<li><p><a href="wia-ipa-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-bits-per-channel.md)"><strong>WIA_IPA_BITS_PER_CHANNEL</strong></a></p></li>
<li><p><a href="wia-ipa-planar.md" data-raw-source="[&lt;strong&gt;WIA_IPA_PLANAR&lt;/strong&gt;](wia-ipa-planar.md)"><strong>WIA_IPA_PLANAR</strong></a></p></li>
<li><p><a href="wia-ipa-pixels-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_PIXELS_PER_LINE&lt;/strong&gt;](wia-ipa-pixels-per-line.md)"><strong>WIA_IPA_PIXELS_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-bytes-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BYTES_PER_LINE&lt;/strong&gt;](wia-ipa-bytes-per-line.md)"><strong>WIA_IPA_BYTES_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-number-of-lines.md" data-raw-source="[&lt;strong&gt;WIA_IPA_NUMBER_OF_LINES&lt;/strong&gt;](wia-ipa-number-of-lines.md)"><strong>WIA_IPA_NUMBER_OF_LINES</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_COLOR_DITHER</p></td>
<td><p>WIA_DATA_COLOR と同じデータが、現在選択されているディザー パターンを使用して、ディザリングする点が異なります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_COLOR_THRESHOLD</p></td>
<td><p>しきい値のデータの色。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_DITHER</p></td>
<td><p>スキャン データは、現在選択されているディザー パターンを使用して、ディザリングされます。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>データを表します強度をスキャンします。 パレットは、深さの固定の等間隔のグレースケールを<a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a>プロパティを指定します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_THRESHOLD</p></td>
<td><p>しきい値は、白黒のデータの 1 ピクセルあたり 1 ビットです。 現在の値を超えるデータ<a href="wia-ips-threshold.md" data-raw-source="[&lt;strong&gt;WIA_IPS_THRESHOLD&lt;/strong&gt;](wia-ips-threshold.md)"> <strong>WIA_IPS_THRESHOLD</strong> </a>ホワイト; に変換されて値がこのデータは、黒に変換されます。</p></td>
</tr>
</tbody>
</table>

 

WIA\_IPA\_DATATYPE プロパティは、アプリケーションの設定時に使用される生のデータ転送の種類を示す使用も、 [ **WIA\_IPA\_形式**](wia-ipa-format.md)プロパティに値 WiaImgFmt\_RAW です。 ドライバーは、WIA を設定する必要があります\_IPA\_DATATYPE プロパティを一連の許可されている値が、アプリケーションを選択できます。

次の表に、WIA で有効な定数\_IPA\_データ型と WIA\_IPA\_WiaImgFmt に形式が設定されている\_RAW です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>データ型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DATA_GRAYSCALE</p></td>
<td><p>データを表します強度をスキャンします。 パレットは、深さの固定の等間隔のグレースケールを<a href="wia-ipa-depth.md" data-raw-source="[&lt;strong&gt;WIA_IPA_DEPTH&lt;/strong&gt;](wia-ipa-depth.md)"> <strong>WIA_IPA_DEPTH</strong> </a>プロパティを指定します。</p>
<p><a href="wia-ipa-raw-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_RAW_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-raw-bits-per-channel.md)"> <strong>WIA_IPA_RAW_BITS_PER_CHANNEL</strong> </a>プロパティを 1 に設定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_BGR</p></td>
<td><p>スキャン データが含まれる ◇ (blue green 赤) の色空間。 完全な色形式は次の WIA プロパティを使用してについて説明します。</p>
<ul>
<li><p><a href="wia-ipa-channels-per-pixel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_CHANNELS_PER_PIXEL&lt;/strong&gt;](wia-ipa-channels-per-pixel.md)"><strong>WIA_IPA_CHANNELS_PER_PIXEL</strong></a></p></li>
<li><p><a href="wia-ipa-bits-per-channel.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BITS_PER_CHANNEL&lt;/strong&gt;](wia-ipa-bits-per-channel.md)"><strong>WIA_IPA_BITS_PER_CHANNEL</strong></a></p></li>
<li><p><a href="wia-ipa-pixels-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_PIXELS_PER_LINE&lt;/strong&gt;](wia-ipa-pixels-per-line.md)"><strong>WIA_IPA_PIXELS_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-bytes-per-line.md" data-raw-source="[&lt;strong&gt;WIA_IPA_BYTES_PER_LINE&lt;/strong&gt;](wia-ipa-bytes-per-line.md)"><strong>WIA_IPA_BYTES_PER_LINE</strong></a></p></li>
<li><p><a href="wia-ipa-number-of-lines.md" data-raw-source="[&lt;strong&gt;WIA_IPA_NUMBER_OF_LINES&lt;/strong&gt;](wia-ipa-number-of-lines.md)"><strong>WIA_IPA_NUMBER_OF_LINES</strong></a></p></li>
</ul>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL を 3 に設定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_CMY</p></td>
<td><p>スキャン データがシアン、マゼンタ、黄 (CMY) 色空間。 完全な色形式は WIA_DATA_RAW_BGR に対して挙げられている同じ WIA プロパティを使用して説明します。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL を 3 に設定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_CMYK</p></td>
<td><p>スキャン データがシアン、マゼンタ、黄、黒 (CMYK) 色空間。 完全な色形式は WIA_DATA_RAW_BGR に対して挙げられている同じ WIA プロパティを使用して説明します。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL は 4 に設定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_RGB</p></td>
<td><p>スキャン データが、赤、緑、青 (RGB) の色空間でします。 WIA_DATA_RAW_BGR のように同じ WIA プロパティを使用して、完全な色の書式がについて説明します。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL を 3 に設定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DATA_RAW_YUV</p></td>
<td><p>スキャン データは、青の輝度違い red 違い (YUV) 色空間。 完全な色形式は WIA_DATA_RAW_BGR に対して挙げられている同じ WIA プロパティを使用して説明します。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL を 3 に設定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DATA_RAW_YUVK</p></td>
<td><p>スキャン データは、青の輝度違い-赤の違い、黒 (YUVK) 色空間。 完全な色形式は WIA_DATA_RAW_BGR に対して挙げられている同じ WIA プロパティを使用して説明します。</p>
<p>WIA_IPA_RAW_BITS_PER_CHANNEL は 4 に設定する必要があります。</p></td>
</tr>
</tbody>
</table>

 

デバイスを 1 つの値に設定すると作成、WIA\_PROP\_リストの種類と、有効な値を配置します。

チェック、 [ **WIA\_IPA\_深さ**](wia-ipa-depth.md)ビット数を決定するプロパティ。

WIA\_IPA\_DATATYPE プロパティには、通常、カメラの単一の値が含まれています。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IPA\_ビット\_1 秒あたり\_チャネル**](wia-ipa-bits-per-channel.md)

[**WIA\_IPA\_バイト\_1 秒あたり\_行**](wia-ipa-bytes-per-line.md)

[**WIA\_IPA\_チャネル\_1 秒あたり\_ピクセル**](wia-ipa-channels-per-pixel.md)

[**WIA\_IPA\_深さ**](wia-ipa-depth.md)

[**WIA\_IPA\_形式**](wia-ipa-format.md)

[**WIA\_IPA\_数\_の\_行**](wia-ipa-number-of-lines.md)

[**WIA\_IPA\_ピクセル\_1 秒あたり\_行**](wia-ipa-pixels-per-line.md)

[**WIA\_IPA\_平面**](wia-ipa-planar.md)

[**WIA\_IPA\_RAW\_ビット\_1 秒あたり\_チャネル**](wia-ipa-raw-bits-per-channel.md)

[**WIA\_IP\_しきい値**](wia-ips-threshold.md)

 

 






