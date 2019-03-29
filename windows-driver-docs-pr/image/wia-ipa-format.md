---
title: WIA\_IPA\_形式
description: WIA\_IPA\_FORMAT プロパティに転送されるイメージの現在の形式が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 5b60b45f-16ad-45c4-97f0-d92099f698b9
keywords:
- WIA_IPA_FORMAT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_FORMAT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2339edf101df144529d99b534d231159c4c950af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581706"
---
# <a name="wiaipaformat"></a>WIA\_IPA\_形式


WIA\_IPA\_FORMAT プロパティに転送されるイメージの現在の形式が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_format_si"></span><span id="DDK_WIA_IPA_FORMAT_SI"></span>


プロパティの種類:VT\_CLSID

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

デバイスを 1 つの値に設定すると作成、WIA\_PROP\_リストの種類、および有効な値を配置します。

Windows 8 と Windows の以降のバージョンでは、次の値に追加された、WIA\_IPA\_形式のプロパティ。

-   WiaImgFmt\_CSV

-   WiaImgFmt\_JBIG2

-   WiaImgFmt\_RawBar

-   WiaImgFmt\_RawMic

-   WiaImgFmt\_RawPat

-   WiaImgFmt\_XmlBar

-   WiaImgFmt\_XmlMic

-   WiaImgFmt\_XmlPat

以降では、Windows Vista および Windows の以降のバージョンは、次の値は、WIA の追加は\_IPA\_形式のプロパティ。

-   WiaImgFmt\_PDFA

-   WiaImgFmt\_JBIG

-   WiaImgFmt\_XPS

両方、WiaImgFmt\_PDFA と WiaImgFmt\_XPS 形式では、ドライバーは、いずれかをサポートする必要があります[ **WIA\_IPA\_圧縮**](wia-ipa-compression.md)値。 これらの 2 つの書式設定、既定 WIA\_IPA\_圧縮値、WIA\_圧縮\_NONE の場合、意味の「定義されていません」。 スキャナー (または、ドライバーの PDF または xps 形式のファイルが生成されます) は、イメージ データに使用される内部圧縮モードを選択する必要があります。

次の表に、WIA で有効な定数\_IPA\_形式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>形式</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WiaAudFmt_AIFF</p></td>
<td><p>AIFF オーディオ形式</p></td>
</tr>
<tr class="even">
<td><p>WiaAudFmt_MP3</p></td>
<td><p>MP3 オーディオの形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaAudFmt_WAV</p></td>
<td><p>WAV のオーディオ形式</p></td>
</tr>
<tr class="even">
<td><p>WiaAudFmt_WMA</p></td>
<td><p>WMA オーディオの形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_ASF</p></td>
<td><p>ASF ビデオ形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_AVI</p></td>
<td><p>AVI ビデオ形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_BMP</p></td>
<td><p>Windows デバイス ・独立ビットマップ (DIB) ファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_CIFF</p></td>
<td><p>カメラの画像ファイル形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_CSV<strong></p></td>
<td><p>コンマ区切りファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_DPOF</p></td>
<td><p>DPOF 印刷形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_EMF</p></td>
<td><p>拡張 Windows メタファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_EXEC</p></td>
<td><p>実行可能ファイル</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_EXIF</p></td>
<td><p>交換ファイル形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_FLASHPIX</p></td>
<td><p>FlashPix 形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_GIF</p></td>
<td><p>GIF イメージ形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_HTML</p></td>
<td><p>HTML 形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_ICO</p></td>
<td><p>Windows アイコン ファイルの形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JBIG*</p></td>
<td><p>共同 Bi-level イメージ専門家グループの形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JBIG2</strong></p></td>
<td><p>共同 Bi-level イメージ専門家グループ形式 (バージョン 2)</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JPEG</p></td>
<td><p>JPEG 圧縮形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JPEG2K</p></td>
<td><p>JPEG 2000 形式の圧縮</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JPEG2KX</p></td>
<td><p>JPEG 2000 形式の圧縮</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_MEMORYBMP</p></td>
<td><p>ヘッダー ファイルを使用せずに Windows ビットマップ</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_MPG</p></td>
<td><p>MPEG ビデオ形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PHOTOCD</p></td>
<td><p>Eastman Kodak ファイルの形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_PDFA<em></p></td>
<td><p>PDF の (ISO/CD 19005-1) の形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PICT</p></td>
<td><p>Apple のファイルの形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_PNG</p></td>
<td><p>W3C PNG 形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RAW</p></td>
<td><p>WIA 生のイメージ ファイル形式のデータ転送のみ</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawBar</em><em></p></td>
<td><p>WIA バーコード メタデータの生の形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RawMic</em><em></p></td>
<td><p>WIA MICR メタデータの生の形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawPat</em><em></p></td>
<td><p>WIA 修正プログラム コードのメタデータの Raw 形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RAWRGB</p></td>
<td><p>RGB の生の形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RTF</p></td>
<td><p>リッチ テキスト ファイルの形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_SCRIPT</p></td>
<td><p>スクリプト ファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_TIFF</p></td>
<td><p>Tagged Image File Format (TIFF)</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_TXT</p></td>
<td><p>テキスト ファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_UNICODE16</p></td>
<td><p>Unicode 16 ビットのエンコーディング</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_WMF</p></td>
<td><p>Windows メタファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XML</p></td>
<td><p>XML ファイル</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_XmlBar</em><em></p></td>
<td><p>WIA バーコードのメタデータのスキーマに準拠してがコンテンツを持つ XML ファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XmlMic</em><em></p></td>
<td><p>WIA MICR メタデータのスキーマに準拠してがコンテンツを持つ XML ファイル</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_XmlPat</em><em></p></td>
<td><p>WIA 修正プログラム コードのメタデータのスキーマに準拠してコンテンツを持つ XML ファイル</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XPS</em></p></td>
<td><p>XPS ドキュメント ファイル</p></td>
</tr>
</tbody>
</table>

 

アスタリスクでマークされている形式 (\*) は、Windows Vista および以降のバージョンの Windows のみです。

2 つのアスタリスクでマークされている形式 (\*\*) は、Windows 8 および以降のバージョンの Windows のみです。

WiaImgFmt は、既定値にこのプロパティの初期値を設定する必要がありますすべて WIA 2.0 ミニドライバー\_BMP です。

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


[**WIA\_IPA\_圧縮**](wia-ipa-compression.md)

[**WIA\_IPA\_完全\_項目\_名**](wia-ipa-full-item-name.md)

 

 






