---
title: WIA\_IPA\_PROP\_ストリーム\_COMPAT\_ID
description: WIA\_IPA\_PROP\_ストリーム\_COMPAT\_ID プロパティを一連のデバイス プロパティの値を表すクラス識別子 (CLSID) を指定します。
ms.assetid: e0701a7a-45e8-4096-8f20-2ed7d3113181
keywords:
- WIA_IPA_PROP_STREAM_COMPAT_ID イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_PROP_STREAM_COMPAT_ID
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1563f77641271777dbfc296527f2049207e6871f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380348"
---
# <a name="wiaipapropstreamcompatid"></a>WIA\_IPA\_PROP\_ストリーム\_COMPAT\_ID


WIA\_IPA\_PROP\_ストリーム\_COMPAT\_ID プロパティを一連のデバイス プロパティの値を表すクラス識別子 (CLSID) を指定します。

## <span id="ddk_wia_ipa_prop_stream_compat_id_si"></span><span id="DDK_WIA_IPA_PROP_STREAM_COMPAT_ID_SI"></span>


プロパティの種類:VT\_CLSID

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

デバイス ドライバーは、WIA を実装している場合\_IPA\_PROP\_ストリーム\_COMPAT\_ID プロパティでは、アプリケーションこのプロパティを使用して、デバイスが一連の値をサポートするかどうかを確認します。

次の表に、WIA で有効な定数\_IPA\_PROP\_ストリーム\_COMPAT\_id。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>表記</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WiaImgFmt_BMP</p></td>
<td><p>ヘッダー ファイルを使用して Microsoft Windows ビットマップ</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_EMF</p></td>
<td><p>拡張 Windows メタファイル</p></td>
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
<td><p>WiaImgFmt_ICO</p></td>
<td><p>Windows アイコン ファイルの形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JPEG</p></td>
<td><p>JPEG 圧縮形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_PHOTOCD</p></td>
<td><p>Eastman Kodak ファイルの形式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PNG</p></td>
<td><p>W3C PNG 形式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_MEMORYBMP</p></td>
<td><p>ヘッダー ファイルを使用せずに Windows ビットマップ</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_TIFF</p></td>
<td><p>イメージ ファイル形式のタグ</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_WMF</p></td>
<td><p>Windows メタファイル</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
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

 

 





