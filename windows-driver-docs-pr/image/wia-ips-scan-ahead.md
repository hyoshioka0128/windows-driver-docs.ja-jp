---
title: WIA\_IP\_スキャン\_AHEAD
description: WIA\_IP\_スキャン\_AHEAD プロパティを使用して、ハードウェア デバイスで最高速度、スキャンした画像を並列でバッファー内のイメージを転送する、スキャナーの内部メモリにバッファリング (スキャンでスキャンを有効にします。クライアント アプリケーションに同じまたは低い速度で)。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 706BA423-399F-4859-BF41-10D3A88B61DD
keywords:
- WIA_IPS_SCAN_AHEAD イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_SCAN_AHEAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: deb7b4eff92044ec81894c26214dd44d193ee8ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343862"
---
# <a name="wiaipsscanahead"></a>WIA\_IP\_スキャン\_AHEAD


**WIA\_IP\_スキャン\_AHEAD**プロパティを使用して、ハードウェア デバイスで最高速度、スキャンした画像をスキャナーの内部のメモリにバッファリング (スキャンでスキャンを有効にします。転送バッファー イメージを同じまたは低い速度でクライアント アプリケーションに並列的に)。 WIA ミニドライバーは、作成し、このプロパティを保持します。




**注**  このプロパティは[ **WIA\_DPS\_スキャン\_AHEAD\_ページ**](wia-dps-scan-ahead-pages.md)は廃止されました。

 

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_スキャン\_AHEAD**プロパティ。

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
<td><p>WIA_SCAN_AHEAD_DISABLED</p></td>
<td><p>事前にスキャンが無効です。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SCAN_AHEAD_ENABLED</p></td>
<td><p>事前にスキャンを有効にするとします。 WIA クライアント アプリケーションには、可能な限り高速でイメージをダウンロードする必要があります。 スキャン ジョブが完了する前に取り消された場合いくつかのスキャンしたドキュメントが失われます (アプリケーションに転送されていない)。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは、フィーダー項目に対してのみ有効です (WIA\_カテゴリ\_フィーダー) は省略可能です。

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

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_SCAN\_AHEAD\_PAGES**](wia-dps-scan-ahead-pages.md)

 

 






