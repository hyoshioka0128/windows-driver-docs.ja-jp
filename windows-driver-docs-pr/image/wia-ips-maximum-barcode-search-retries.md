---
title: WIA\_IP\_最大\_バーコード\_検索\_再試行
description: WIA\_IP\_最大\_バーコード\_検索\_再試行プロパティは、バーコードが見つからないバーコードの検出が有効になっている場合、リーダーが試行の再試行の最大数をについて説明します。
ms.assetid: AA9255D2-6B3B-4539-8C9C-7B0B84E2417D
keywords:
- WIA_IPS_MAXIMUM_BARCODE_SEARCH_RETRIES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_MAXIMUM_BARCODE_SEARCH_RETRIES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 08cf90984ff258a20fc061c04d6cf78d65d415ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571276"
---
# <a name="wiaipsmaximumbarcodesearchretries"></a>WIA\_IP\_最大\_バーコード\_検索\_再試行


**WIA\_IP\_最大\_バーコード\_検索\_再試行**プロパティは、バーコードが見つからない場合に、リーダーが試みる再試行の最大数を示します。バーコードの検出を有効にします。



プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

このプロパティは、バーコード リーダーのすべての項目に必要です。 プロパティは、0 (再試行なし) を含む、1 つ 1 つの値を含む範囲をサポートするために実装できます。

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

 

 





