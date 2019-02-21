---
title: WIA\_IP\_MICR\_リーダー
description: WIA ミニドライバーは、WIA\_IP\_MICR\_磁気インク文字認識 (MICR) リーダーが使用可能な場所を報告するリーダー プロパティ。 WIA クライアント アプリケーションは、MICR 検出を有効にする次の場所のいずれかを選択できます。
ms.assetid: 093A5EDF-BFD6-42BD-B532-9CB578EA284C
keywords:
- WIA_IPS_MICR_READER イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_MICR_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c84bcf1512604082fecdbfcdd381c0da7553488b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528431"
---
# <a name="wiaipsmicrreader"></a>WIA\_IP\_MICR\_リーダー


WIA ミニドライバーを使用して、 **WIA\_IP\_MICR\_リーダー**磁気インク文字認識 (MICR) リーダーが使用可能な場所を報告するプロパティ。 WIA クライアント アプリケーションは、MICR 検出を有効にする次の場所のいずれかを選択できます。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表に、必要な値を**WIA\_IP\_MICR\_リーダー**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MICR_READER_DISABLED</p></td>
<td><p>MICR 検出は無効です。 これは、必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_AUTO</p></td>
<td><p>MICR の検出を有効にします。 MICR リーダーの位置は固定またはアクティブなスキャンの入力ソースによって実行時にデバイスが自動的に選択します。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは、MICR リーダーのすべての項目に必要です。 WIA\_MICR\_リーダー\_無効になり、WIA\_MICR\_リーダー\_自動値が必要です。 WIA\_MICR\_リーダー\_無効になっていますが、必要な既定値。

次の表の省略可能な値、 **WIA\_IP\_MICR\_リーダー**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MICR_READER_FLATBED</p></td>
<td><p>MICR 検出では、フラット ベッドにスキャンしたドキュメントを有効にします。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_FEEDER_FRONT</p></td>
<td><p>MICR 検出では、フィーダーをスキャンしたドキュメントのフロント サイドを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MICR_READER_FEEDER_BACK</p></td>
<td><p>MICR 検出では、フィーダーをスキャンしたドキュメントのフロント サイドを有効にします。</p></td>
</tr>
<tr class="even">
<td><p>WIA_MICR_READER_FEEDER_DUPLEX</p></td>
<td><p>両方のフロント サイド MICR 検出を有効にして、フィーダーをスキャンしたドキュメントの背面にあります。</p></td>
</tr>
</tbody>
</table>

 

**注**  WIA ミニドライバーは省略可能な値のプロパティの構成を受け入れる、スキャン時に非アクティブなスキャンの入力ソース MICR 検出を有効にする要求を無視するだけに許可されています。

 

[ **WIA\_IPA\_形式**](wia-ipa-format.md)も MICR リーダーのすべての項目の必須プロパティです。

次の表に、必要な値を[ **WIA\_IPA\_形式**](wia-ipa-format.md) MICR リーダー項目で実装されているときに、プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WiaImgFmt_XmlMic</p></td>
<td><p>MICR メタデータは、コンテンツを持つ、WIA MICR メタデータのスキーマに準拠して XML ファイルとして転送されます。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawMic</p></td>
<td><p>MICR メタデータは、WIA MICR メタデータの生の形式のファイルとして転送されます。</p></td>
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

 

 





