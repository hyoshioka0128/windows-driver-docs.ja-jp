---
title: WIA\_IPA\_圧縮
description: WIA\_IPA\_圧縮プロパティに使用される現在の圧縮の種類が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 6853dc51-bde0-4548-92f6-678b55cf6275
keywords:
- WIA_IPA_COMPRESSION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_COMPRESSION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbca734cb6848f23608573f3be77e326b9212d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369562"
---
# <a name="wiaipacompression"></a>WIA\_IPA\_圧縮


WIA\_IPA\_圧縮プロパティに使用される現在の圧縮の種類が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_compression_si"></span><span id="DDK_WIA_IPA_COMPRESSION_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み (イメージの取得)。読み取り専用 (イメージのストレージ)

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_IPA\_イメージの圧縮の種類またはアプリケーションを決定する圧縮プロパティは、圧縮設定を構成するには、このプロパティを設定します。

次の表に、WIA で有効な定数\_IPA\_圧縮します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_COMPRESSION_BI_RLE4</p></td>
<td><p>RLE 4 圧縮</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_BI_RLE8</p></td>
<td><p>RLE 8 圧縮</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_G3</p></td>
<td><p>グループ 3 の圧縮</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_G4</p></td>
<td><p>グループ 4 の圧縮</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_JBIG<em></p></td>
<td><p>11544 (ITU-T T.82) 圧縮します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_JPEG</p></td>
<td><p>JPEG 圧縮</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_JPEG2K</em></p></td>
<td><p>JPEG 2000 の圧縮</p></td>
</tr>
<tr class="even">
<td><p>WIA_COMPRESSION_NONE</p></td>
<td><p>圧縮なし</p></td>
</tr>
<tr class="odd">
<td><p>WIA_COMPRESSION_PNG*</p></td>
<td><p>W3C PNG 圧縮</p></td>
</tr>
</tbody>
</table>

 

アスタリスクでマークされている値 (\*) は、Windows Vista およびそれ以降のオペレーティング システムのみです。

**注**   WiaImgFmt ファイル形式の場合\_XPS または WiaImgFmt\_PDFA、WIA\_圧縮\_NONE は、「未定義」を意味します (ある場合)、デバイスは内部の圧縮を選択できません。これら 2 つのドキュメントの形式で格納されているイメージ。

 

すべて WIA 2.0 ミニドライバーは、WIA が既定値にこのプロパティの初期値を設定する必要があります\_圧縮\_NONE。

アクセス権、WIA\_IPA\_圧縮プロパティは読み取り/書き込みにすべてのイメージが保存されている画像項目の読み取り専用の取得。

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

 

 





