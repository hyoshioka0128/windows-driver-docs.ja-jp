---
title: WIA\_IP\_プレビュー
description: WIA\_IP\_プレビュー プロパティは、デバイスのプレビュー モードを示します。
ms.assetid: 06caadc7-2a65-4c54-8d63-4aa1c17186de
keywords:
- WIA_IPS_PREVIEW イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PREVIEW
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebde67ca6fa81701d2c0b7d5b72643fddecd9144
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372333"
---
# <a name="wiaipspreview"></a>WIA\_IP\_プレビュー


WIA\_IP\_プレビュー プロパティは、デバイスのプレビュー モードを示します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーション設定 WIA\_IP\_プレビューをプレビュー モードにデバイスを配置します。

次の表に、WIA で有効な定数\_IP\_プレビューします。

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
<td><p>WIA_FINAL_SCAN</p></td>
<td><p>アプリケーションでは、最後のスキャンを実行します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PREVIEW_SCAN</p></td>
<td><p>アプリケーションでは、プレビューのスキャンを実行します。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_PREVIEW プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_プレビュー**](wia-dps-preview.md)

 

 






