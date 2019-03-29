---
title: WIA\_IP\_ジョブ\_区切り記号
description: WIA\_IP\_ジョブ\_のジョブの区切り記号の検出を有効にして、ジョブ区切りページを検出したときに、デバイスが実行されるアクションを構成する区切り記号のプロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 2ECD88EB-2B6F-477D-8F37-D4EECA580FAE
keywords:
- WIA_IPS_JOB_SEPARATORS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_JOB_SEPARATORS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c3dfb8a5f462f1374761fe5bea27fd3b6fc64d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572883"
---
# <a name="wiaipsjobseparators"></a>WIA\_IP\_ジョブ\_区切り記号


**WIA\_IP\_ジョブ\_区切り記号**のジョブの区切り記号の検出を有効にして、ジョブ区切りページを検出したときに、デバイスが実行されるアクションを構成するプロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

次の表に、有効な値、 **WIA\_IP\_ジョブ\_区切り記号**プロパティ。

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
<td><p>WIA_SEPARATOR_DISABLED</p></td>
<td><p>ジョブの区切り記号の検出は無効です。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SEPARATOR_DETECT_SCAN_CONTINUE</p></td>
<td><p>検出ジョブの区切り記号 ページ、区切りページをスキャンし、スキャンを続行します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_SEPARATOR_DETECT_SCAN_STOP</p></td>
<td><p>検出ジョブの区切り記号 ページ、区切りページをスキャンし、スキャンを停止します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SEPARATOR_DETECT_NOSCAN_CONTINUE</p></td>
<td><p>ジョブ区切りページを検出、操作を行いましていないスキャン (スキップ)、区切り記号 ページで、スキャンを継続しています。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_SEPARATOR_DETECT_NOSCAN_STOP</p></td>
<td><p>検出ジョブの区切り記号 ページ、ありません (スキップ)、区切り記号のページをスキャンしてくださいスキャンを停止します。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは省略可能で、フィーダー付きのデータ ソース アイテムにのみ有効です (で表される、 [ **WIA\_IPA\_項目\_カテゴリ**](wia-ipa-item-category.md)として WIAプロパティ\_カテゴリ\_フィーダー)。

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

 

 





