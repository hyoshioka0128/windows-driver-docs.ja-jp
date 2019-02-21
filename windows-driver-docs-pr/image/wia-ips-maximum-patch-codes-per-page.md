---
title: WIA\_IP\_最大\_PATCH\_コード\_1 秒あたり\_ページ
description: WIA\_IP\_最大\_PATCH\_コード\_1 秒あたり\_ページのプロパティは、1 つのドキュメント ページにある、デバイスが検出する必要があり、できる修正プログラム コードの最大数をについて説明しますと修正プログラム コードの検出が有効になっているとします。
ms.assetid: 91A0DAC0-D8F3-48BB-9DD4-AF50BD8F09AB
keywords:
- WIA_IPS_MAXIMUM_PATCH_CODES_PER_PAGE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_PATCH_CODES_PER_PAGE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 413b47d857d390f4b7a345368785b32f79d5fae9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549443"
---
# <a name="wiaipsmaximumpatchcodesperpage"></a>WIA\_IP\_最大\_PATCH\_コード\_1 秒あたり\_ページ


**WIA\_IP\_最大\_PATCH\_コード\_1 秒あたり\_ページ**プロパティは、デバイスがしたりする必要がある修正プログラム コードの最大数を示します。修正プログラム コードの検出が有効にすると、1 つのドキュメント ページにある検出します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

値 0 は、「最大値なし」を意味します。 アプリケーションは、修正プログラム コードの検出に費やされた時間を短縮するためにこのプロパティの現在の値を小さくと、スキャンの速度を上げます。

このプロパティは必須の修正プログラム コード リーダーのすべての項目が、0 (最小等しい最大値、およびステップ サイズは 0、0 に設定すると) の値のみを含む範囲コンテナーとして実装できます。

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

 

 





