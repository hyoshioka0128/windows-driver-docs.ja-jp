---
title: WIA\_IP\_自動\_トリミング
description: WIA\_IP\_自動\_トリミング プロパティを使用して自動的に検出し、スキャンのリージョンのデバイスによってトリミングを有効にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 5D7D2911-1535-4E67-9EBF-2B59D87F4F1B
keywords:
- WIA_IPS_AUTO_CROP イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_AUTO_CROP
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7612e7ddc6065b74b7ea6581ea25eabd50f3b331
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381504"
---
# <a name="wiaipsautocrop"></a>WIA\_IP\_自動\_トリミング


**WIA\_IP\_自動\_トリミング**プロパティを使用して自動的に検出し、スキャンのリージョンのデバイスによってトリミングを有効にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_自動\_トリミング**プロパティ。

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
<td><p>WIA_AUTO_CROP_DISABLED</p></td>
<td><p>自動トリミングが無効です。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_AUTO_CROP_SINGLE</p></td>
<td><p>自動トリミングが有効になっているとします。 スキャンの 1 つのリージョンが検出され、各ドキュメントのページでトリミングされます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_AUTO_CROP_MULTI</p></td>
<td><p>自動トリミングが有効になっているとします。 1 つまたは複数のスキャンのリージョンが検出され、各ドキュメントのページでトリミングされます。 各スキャンのトリミングされたリージョンは、1 ページのファイルを 1 つまたは複数ページのファイルに新しいページとして WIA アプリケーションのクライアントに転送されます。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは有効であり、フィーダーの省略可能な (WIA\_カテゴリ\_フィーダー) を実装すること、WIA の有無項目\_ページ\_の自動値、 [ **WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)プロパティ。 このプロパティは有効な (および省略可能) ではまた、フラット ベッドの (WIA\_カテゴリ\_ベッド) とフィルム (WIA\_カテゴリ\_フィルム) 項目、のみ、wiaWIAミニドライバーによってセグメント化がサポートされていない場合\_カテゴリ\_ベッドと WIA\_カテゴリ\_フィルムの入力ソース。 場合 WIA\_IP\_SEGEMENTATION がサポートされている、WIA\_IP\_自動\_トリミングが無効であると同時にサポートすることはできません。

プロパティがサポートされている、WIA\_自動\_トリミング\_無効になっていると、その他の 2 つの可能な値の 1 つ以上 (WIA\_自動\_トリミング\_単一や WIA\_自動\_トリミング\_マルチ) が必要な WIA\_自動\_トリミング\_必要な既定を無効になっています。

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

 

 





