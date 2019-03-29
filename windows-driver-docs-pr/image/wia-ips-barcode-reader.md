---
title: WIA\_IP\_バーコード\_リーダー
description: WIA\_IP\_バーコード\_リーダー プロパティは、使用可能なバーコード リーダーの場所を一覧表示する WIA ミニドライバーによって使用されます (1/固定または複数) とアプリケーション クライアントがこれらの場所のいずれかを選択し、バーコードを有効にします。検出します。
ms.assetid: EED6CE6D-38CC-4368-8722-5765849C5A7D
keywords:
- WIA_IPS_BARCODE_READER イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_READER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7756efebdc0cbb919d85c38649e38db087cd79b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580018"
---
# <a name="wiaipsbarcodereader"></a>WIA\_IP\_バーコード\_リーダー


**WIA\_IP\_バーコード\_リーダー**プロパティは、使用可能なバーコード リーダーの場所を一覧表示する WIA ミニドライバーによって使用されます (1/固定または複数) と、アプリケーションのクライアントのいずれかを選択するにはこれらの場所とバーコードの検出を有効にします。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

次の表に、必要な値を**WIA\_IP\_バーコード\_リーダー**プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>[値]</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_BARCODE_READER_DISABLED</p></td>
<td><p>バーコードの検出は無効です。 これは、必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_AUTO</p></td>
<td><p>バーコードの検出を有効にします。 バーコード リーダーの位置は、アクティブなスキャンの入力ソースによって実行時に、デバイスで自動的に選択されます。</p></td>
</tr>
</tbody>
</table>

 

次の表の省略可能な値、 **WIA\_IP\_バーコード\_リーダー**プロパティ。

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
<td><p>WIA_BARCODE_READER_FLATBED</p></td>
<td><p>バーコードの検出には、フラット ベッド スキャナーでスキャンされたドキュメントを有効にします。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_FEEDER_FRONT</p></td>
<td><p>バーコードの検出には、スキャナー フィーダーにスキャンされたドキュメントのフロント サイドを有効にします。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_READER_FEEDER_BACK</p></td>
<td><p>バーコードの検出には、スキャナー フィーダーにスキャンされたドキュメントのフロント サイドを有効にします。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_READER_FEEDER_DUPLEX</p></td>
<td><p>バーコードの検出を有効にします。 バーコード リーダーの位置は、アクティブなスキャンの入力ソースによって実行時に、デバイスで自動的に選択されます。</p></td>
</tr>
</tbody>
</table>

 

**注**  WIA ミニドライバーは省略可能な値のプロパティの構成を受け入れる、スキャン時に非アクティブなスキャンの入力ソースにバーコードの検出を有効にする要求を無視するだけに許可されています。

 

このプロパティは、バーコード リーダーのすべての項目に必要です。 WIA\_バーコード\_リーダー\_無効になり、WIA\_バーコード\_リーダー\_自動値が必要です。 WIA\_バーコード\_リーダー\_無効になっていますが、必要な既定値。

[ **WIA\_IPA\_形式**](wia-ipa-format.md)もバーコード リーダーのすべての項目の必須プロパティです。

次の表に、必要な値を[ **WIA\_IPA\_形式**](wia-ipa-format.md)バーコード リーダー項目で実装されているときに、プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>[値]</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WiaImgFmt_XmlBar</p></td>
<td><p>バーコードのメタデータは、コンテンツを持つ、WIA バーコードのメタデータのスキーマに準拠して XML ファイルとして転送されます。</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawBar</p></td>
<td><p>バーコードのメタデータは、WIA バーコード メタデータの生の形式のファイルとして転送されます。</p></td>
</tr>
</tbody>
</table>

 

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

 

 





