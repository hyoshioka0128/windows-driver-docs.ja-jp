---
title: WIA\_IP\_プリンター\_裏書き\_最大\_グラフィック
description: WIA\_IP\_プリンター\_裏書き\_最大\_グラフィックス プロパティは、各ページに・ インプリント ・/裏書き項目が印刷または推奨するイメージの最大数をについて説明します。
ms.assetid: A8FB39D2-659C-45E9-BE5E-627E594B9D3A
keywords:
- WIA_IPS_PRINTER_ENDORSER_MAX_GRAPHICS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_MAX_GRAPHICS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eee3c72973bdbbd14bff590f8ad6199629962238
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351129"
---
# <a name="wiaipsprinterendorsermaxgraphics"></a>WIA\_IP\_プリンター\_裏書き\_最大\_グラフィック


**WIA\_IP\_プリンター\_裏書き\_最大\_グラフィックス**プロパティは、・ インプリント ・/裏書き項目を印刷するイメージの最大数を説明しますまたは。各ページに保証します。 このプロパティは、・ インプリント ・/裏書き項目が複数ページを使用してグラフィックスのアップロードをサポートしている場合に便利です (TYMED\_マルチページ\_ファイル) ファイル形式の転送。 このプロパティは初期化され、WIA ミニ ドライバーによって保持され、Windows 8 および Windows の以降のバージョンで利用できます。

プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

**WIA\_IP\_プリンター\_裏書き\_最大\_グラフィックス**プロパティは、グラフィックスをサポートしている・ インプリント ・/裏書き項目のアップロードの省略可能です。 実装された場合、プロパティ値**あります**ゼロ (0) より大きい。

TYMED の詳細については\_マルチページ\_ファイル定数を参照してください[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)します。

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


[**WIA\_IPA\_TYMED**](wia-ipa-tymed.md)

 

 






