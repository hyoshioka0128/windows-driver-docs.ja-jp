---
title: WIA\_IP\_バーコード\_検索\_タイムアウト
description: WIA\_IP\_バーコード\_検索\_TIMEOUT プロパティは、ドキュメントのページでのバーコードを検索する最長時間をについて説明します。
ms.assetid: 3EE6C492-722E-439A-8BB5-03496DAC78D2
keywords:
- WIA_IPS_BARCODE_SEARCH_TIMEOUT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_SEARCH_TIMEOUT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: df86fce0ce3ceeebd250349b52365058ba270d8f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370634"
---
# <a name="wiaipsbarcodesearchtimeout"></a>WIA\_IP\_バーコード\_検索\_タイムアウト


**WIA\_IP\_バーコード\_検索\_タイムアウト**プロパティは、ドキュメントのページでのバーコードを検索する最長時間をについて説明します。


プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

時間の単位が指定されていない (ことができます (ミリ秒) または、1 秒の 1/10 など) が、アプリケーション値を選択できます: 最小最大範囲は、WIA ミニドライバーによって報告されました。

このプロパティは、バーコード リーダーのすべての項目に必要です。 プロパティは、1 つの 1 つの値 (つまり、アプリケーションがこのタイムアウトを変更することはできません) が含まれている範囲をサポートするために実装できます。

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

 

 





