---
title: WIA\_IP\_プリンター\_裏書き\_パディング
description: WIA\_IP\_プリンター\_裏書き\_PADDING プロパティは、印刷またはカウンターで空白のスペースを埋めるの動作保証済みされる有効な特別な埋め込み文字を構成します。 データと時刻のシーケンス。
ms.assetid: 44C8A517-43E5-4986-9B8A-46167B5884E5
keywords:
- WIA_IPS_PRINTER_ENDORSER_PADDING イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_PADDING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0f52676394c3e28b56f5ed15195225a4d46171c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351141"
---
# <a name="wiaipsprinterendorserpadding"></a>WIA\_IP\_プリンター\_裏書き\_パディング


**WIA\_IP\_プリンター\_裏書き\_PADDING**プロパティは、印刷またはデータのカウンターで空白のスペースを埋めるの動作保証済みされる有効な特別な埋め込み文字を構成します。時刻のシーケンス。 このプロパティは初期化され、WIA ミニ ドライバーによって保持され、Windows 8 および Windows の以降のバージョンで利用できます。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

このプロパティの有効な値は、次の表に表示されます。

| 値                      | 説明                                        |
|----------------------------|----------------------------------------------------|
| WIA\_印刷\_PADDING\_NONE  | パディングなし。                                        |
| WIA\_印刷\_PADDING\_0  | 数字のゼロ (0) は、埋め込み文字として使用されます。 |
| WIA\_印刷\_PADDING\_空白 | 空白 (空白) 文字は、パディングに使用されます。   |

 

**WIA\_IP\_プリンター\_裏書き\_PADDING**プロパティは・ インプリント ・/裏書き項目のオプションです。 このプロパティがサポートされていない場合、プリンター/裏書きデバイスは、埋め込みをサポートしていません。

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

 

 





