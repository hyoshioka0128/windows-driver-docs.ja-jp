---
title: WIA\_IP\_最大\_バーコード\_1 秒あたり\_ページ
description: WIA\_IP\_最大\_バーコード\_1 秒あたり\_バーコードの検出が有効にすると、ページ プロパティが 1 つのドキュメント ページにある、デバイスが検出する必要があり、できるをバーコードの最大数を示します.
ms.assetid: 9DA59D24-3483-4663-8B6A-54EC53A3466D
keywords:
- WIA_IPS_MAXIMUM_BARCODES_PER_PAGE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_BARCODES_PER_PAGE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: cbf8b863d500a9c39593ecb8b39777a1983d6da7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571641"
---
# <a name="wiaipsmaximumbarcodesperpage"></a>WIA\_IP\_最大\_バーコード\_1 秒あたり\_ページ


**WIA\_IP\_最大\_バーコード\_1 秒あたり\_ページ**プロパティは、1 つのドキュメントで、デバイスが検出する必要があり、できるをバーコードの最大数をについて説明しますページ側バーコードの検出が有効にするとします。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

0 の値は、"maximum ありません" アプリケーションは、バーコードの検出に費やされた時間を短縮するためにこのプロパティの現在の値を小さくと、スキャンの速度を上げます。

このプロパティが必要ですが、バーコード リーダーのすべてのアイテムの 0 (最小等しい最大値、およびステップ サイズは 0、0 に設定すると) の値のみを含む範囲コンテナーとして実装できます。

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

 

 





