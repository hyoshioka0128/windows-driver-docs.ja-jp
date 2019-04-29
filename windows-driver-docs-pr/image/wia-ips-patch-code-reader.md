---
title: WIA\_IP\_PATCH\_コード\_リーダー
description: WIA\_IP\_PATCH\_コード\_リーダー プロパティを使用して、修正プログラム コードの検出を有効にします。 このプロパティは修正プログラム コード リーダー項目をすべての必須です。
ms.assetid: 8F008388-9822-44DC-B022-0822A8204740
keywords:
- WIA_IPS_PATCH_CODE_READER イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PATCH_CODE_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af4759ba33817370d270d27063daacb641c235c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331361"
---
# <a name="wiaipspatchcodereader"></a>WIA\_IP\_PATCH\_コード\_リーダー


**WIA\_IP\_PATCH\_コード\_リーダー**プロパティを使用して、修正プログラム コードの検出を有効にします。 このプロパティは修正プログラム コード リーダー項目をすべての必須です。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

次の表に、必要な値を**WIA\_IP\_PATCH\_コード\_リーダー**プロパティ。

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
<td><p>WIA_PATCH_CODE_READER_DISABLED</p></td>
<td><p>修正プログラム コードの検出は無効です。 これは、必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_READER_AUTO</p></td>
<td><p>修正プログラム コードの検出が有効になっているとします。 修正プログラム コード リーダーの位置はアクティブなスキャンの入力ソースによって実行時にデバイスで自動的に選択します。</p></td>
</tr>
</tbody>
</table>

 

[ **WIA\_IPA\_形式**](wia-ipa-format.md)プロパティもすべての修正プログラム コード リーダー項目に対して必要です。

次の表に、必要な値を[ **WIA\_IPA\_形式**](wia-ipa-format.md)修正プログラム コード リーダー項目で実装されているときに、プロパティ。

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
<td><p>WiaImgFmt_XmlPat</p></td>
<td><p>修正プログラム コードのメタデータは、WIA 修正プログラム コードのメタデータのスキーマに準拠してがコンテンツを持つ XML ファイルとして転送されます。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawPat</p></td>
<td><p>修正プログラム コードのメタデータは、WIA 修正プログラム コードのメタデータの Raw 形式のファイルとして転送されます。</p></td>
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

 

 





