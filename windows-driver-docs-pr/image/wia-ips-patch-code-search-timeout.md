---
title: WIA\_IP\_PATCH\_コード\_検索\_タイムアウト
description: WIA\_IP\_PATCH\_コード\_検索\_TIMEOUT プロパティは、ドキュメントのページで、修正プログラム コードを検索する最長時間をについて説明します。
ms.assetid: D7DD05B2-43CA-484F-8207-4ED9C307D3AA
keywords:
- WIA_IPS_PATCH_CODE_SEARCH_TIMEOUT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PATCH_CODE_SEARCH_TIMEOUT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf882dd97c4cad00df3e3f6debb08b9d8cb2980
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383683"
---
# <a name="wiaipspatchcodesearchtimeout"></a>WIA\_IP\_PATCH\_コード\_検索\_タイムアウト


**WIA\_IP\_PATCH\_コード\_検索\_タイムアウト**プロパティは、ドキュメントのページで、修正プログラム コードを検索する最長時間をについて説明します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

時間の単位が指定されていない (ことができます (ミリ秒) またはの秒部分の 1/10 など) が、アプリケーション値を選択できます: 最小最大範囲は、WIA ミニドライバーによって報告されました。

このプロパティは、修正プログラム コード リーダーのすべての項目に必要です。 (つまり、アプリケーションは、このタイムアウトを変更できません)、1 つ 1 つの値を含む範囲をサポートするために、プロパティを実装することができます。

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

 

 





