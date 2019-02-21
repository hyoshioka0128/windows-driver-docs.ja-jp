---
title: WIA\_IP\_プリンター\_裏書き\_カウンター
description: WIA\_IP\_プリンター\_裏書き\_カウンター プロパティを使用して、構成、開始値と新しい WIA アプリケーション セッションの先頭に手順・ インプリント ・/裏書きカウンターをインクリメントします。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 3475A0DF-58EA-4B05-96EA-5BBE44655DB0
keywords:
- WIA_IPS_PRINTER_ENDORSER_COUNTER イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_COUNTER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: a680fed0b15f3ff5397acb612e87b36128fdc07d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528164"
---
# <a name="wiaipsprinterendorsercounter"></a>WIA\_IP\_プリンター\_裏書き\_カウンター


**WIA\_IP\_プリンター\_裏書き\_カウンター**プロパティを使用して、開始値とインクリメント手順の先頭に・ インプリント ・/裏書きカウンターの構成新しい WIA アプリケーション セッションです。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

必須の既定値、 **WIA\_IP\_プリンター\_裏書き\_カウンター**プロパティは 0 (最初のページ)。

値の範囲の手順では、(、ミニドライバーは、各ドキュメントのページにスキャンした後、この値をインクリメント)、プリンター/裏書きカウンターの値の増分値について説明します。 このカウンターの手順はさまざまな目的があり、混同しないようにを通じて構成可能な手順で、 [ **WIA\_IP\_プリンター\_裏書き\_手順**](wia-ips-printer-endorser-step.md)プロパティ。

このプロパティは、・ インプリント ・/裏書きデータ ソースのすべてのアイテムでサポートする必要があります。 値 0 (最初のページ) が必要です。

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

 

 





