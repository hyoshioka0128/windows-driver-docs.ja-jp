---
title: WIA\_IP\_プリンター\_裏書き\_有効\_文字
description: WIA\_IP\_プリンター\_裏書き\_有効\_文字プロパティ、WIA に対して有効な文字 (英字、数字、句読点、およびなど) の一覧\_のipアドレス\_プリンター\_裏書き\_・ インプリント ・/機能の構成可能な文字列値。
ms.assetid: 763355B8-7CA0-4B3F-87B1-BD51F24CF78C
keywords:
- WIA_IPS_PRINTER_ENDORSER_VALID_CHARACTERS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_VALID_CHARACTERS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c65c9ab5bbdf94c3d4d2859910cfa9f003b95c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360036"
---
# <a name="wiaipsprinterendorservalidcharacters"></a>WIA\_IP\_プリンター\_裏書き\_有効\_文字


**WIA\_IP\_プリンター\_裏書き\_有効\_文字**プロパティが有効な文字 (英字、数字、句読点、およびなど) を一覧表示[ **WIA\_IP\_プリンター\_裏書き\_文字列**](wia-ips-printer-endorser-string.md) ・ インプリント ・/機能の構成可能な値。 有効な文字のセットは、NULL で終わる文字列として指定されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。




**注**  このプロパティは[ **WIA\_DPS\_裏書き\_文字**](wia-dps-endorser-characters.md)は廃止されました。

 

プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

・ インプリント ・/裏書きのすべての項目で発生するすべての文字をサポートする必要があります、 [ **WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子**](wia-ips-printer-endorser-valid-format-specifiers.md)値 (ある場合)、'$' 文字を含むです。 ・ インプリント ・/機能、WiaImgFmt をサポートしている場合\_の CSV 値[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)、'、' (コンマ) 文字をで表示されない必要があります**WIA\_IP\_プリンター\_裏書き\_有効\_文字**します。

このプロパティは・ インプリント ・/裏書きデータ ソース アイテムをすべて省略可能です。

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


[**WIA\_DPS\_裏書き\_文字**](wia-dps-endorser-characters.md)

[**WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子**](wia-ips-printer-endorser-valid-format-specifiers.md)

 

 






