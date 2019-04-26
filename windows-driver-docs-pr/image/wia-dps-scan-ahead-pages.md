---
title: WIA\_DPS\_スキャン\_AHEAD\_ページ
description: WIA\_DPS\_スキャン\_AHEAD\_ページのプロパティには、スキャナーがアプリケーションに送信する前にスキャナー バッファー内のページをキャッシュするかどうかを示す値が含まれています。
ms.assetid: 8c00b029-dc9f-43e1-af4a-088e143351ca
keywords:
- WIA_DPS_SCAN_AHEAD_PAGES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_SCAN_AHEAD_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f790ff1ac1c5ea87bf6a073c411b70ad7adbae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353861"
---
# <a name="wiadpsscanaheadpages"></a>WIA\_DPS\_スキャン\_AHEAD\_ページ


WIA\_DPS\_スキャン\_AHEAD\_ページのプロパティには、スキャナーがアプリケーションに送信する前にスキャナー バッファー内のページをキャッシュするかどうかを示す値が含まれています。

## <span id="ddk_wia_dps_scan_ahead_pages_si"></span><span id="DDK_WIA_DPS_SCAN_AHEAD_PAGES_SI"></span>


**注**  このプロパティは廃止されました。 使用[ **WIA\_IP\_スキャン\_AHEAD** ](wia-ips-scan-ahead.md)代わりにします。

 

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_(ドキュメント フィーダーが保持できるページの最大数をゼロ) からの範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

場合、WIA\_DPS\_スキャン\_AHEAD\_ページのプロパティが 0、事前にスキャンが無効になっているおよびスキャナーがスキャン先のページ。

スキャナーは、バッファー内のスキャン先読み項目のデータ転送を実行する場合、スキャナーは、バッファー内のページを取得します。 WIA プロパティは、スキャン先読み操作中に変更できません。 WIA\_DPS\_スキャン\_AHEAD\_ページは省略可能です。

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


[**WIA\_IP\_スキャン\_AHEAD**](wia-ips-scan-ahead.md)

 

 






