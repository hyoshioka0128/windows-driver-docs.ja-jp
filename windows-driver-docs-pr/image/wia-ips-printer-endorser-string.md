---
title: WIA\_IP\_プリンター\_裏書き\_文字列
description: WIA\_IP\_プリンター\_裏書き\_文字列プロパティは、テキストが印刷/動作保証済みの構成に使用されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: DF4B1361-EC9C-4BEA-97F5-9179DCB77044
keywords:
- WIA_IPS_PRINTER_ENDORSER_STRING イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_STRING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a30b966b37d4b29fea63899f3f51e9c2f80d625a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351132"
---
# <a name="wiaipsprinterendorserstring"></a>WIA\_IP\_プリンター\_裏書き\_文字列


**WIA\_IP\_プリンター\_裏書き\_文字列**プロパティは、テキストが印刷/動作保証済みの構成に使用されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。




**注**  このプロパティは[ **WIA\_DPS\_裏書き\_文字列**](wia-dps-endorser-string.md)は廃止されました。

 

プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

印刷動作保証済みのテキストは、1 つまたは複数の文字の文字列で表現できます。 各文字の文字列が 1 つまたは複数の特殊文字を使用してで説明されているシーケンスを書式設定を含めることができます、 [ **WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子**](wia-ips-printer-endorser-valid-format-specifiers.md)プロパティ。 文字の文字列で指定された文字のみを含める必要があります[ **WIA\_IP\_プリンター\_裏書き\_有効\_文字**](wia-ips-printer-endorser-valid-characters.md)する NULL 終了する必要があります。 複数の文字の文字列が構成されている場合、WIA ミニドライバーする必要があります印刷/保証 (文字列のリストの繰り返し) 新しいページには、各文字列。

このプロパティは・ インプリント ・/裏書きデータ ソース アイテムをすべて省略可能です。

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

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_裏書き\_文字列**](wia-dps-endorser-string.md)

 

 






