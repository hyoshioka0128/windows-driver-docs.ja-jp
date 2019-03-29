---
title: WIA\_DPS\_裏書き\_文字
description: WIA\_DPS\_裏書き\_文字プロパティには、有効な裏書き文字列を作成するアプリケーションが使用できる有効な文字がすべて含まれます。
ms.assetid: 7bf0676b-df85-486b-a448-ab7275ac846d
keywords:
- WIA_DPS_ENDORSER_CHARACTERS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_ENDORSER_CHARACTERS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dd3008879a607eee4cb494c93b53dd96a74ae06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570659"
---
# <a name="wiadpsendorsercharacters"></a>WIA\_DPS\_裏書き\_文字


WIA\_DPS\_裏書き\_文字プロパティには、有効な裏書き文字列を作成するアプリケーションが使用できる有効な文字がすべて含まれます。

## <span id="ddk_wia_dps_endorser_characters_si"></span><span id="DDK_WIA_DPS_ENDORSER_CHARACTERS_SI"></span>


**注**  このプロパティは廃止されました。 使用[ **WIA\_IP\_プリンター\_裏書き\_有効\_文字**](wia-ips-printer-endorser-valid-characters.md)代わりにします。

 

プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

「承認者」は、スキャナーがスキャンされる各ページにテキスト メッセージについているにインストールされているプリンターです。 WIA ミニドライバーの設定を検証する必要があります、 [ **WIA\_DPS\_裏書き\_文字列**](wia-dps-endorser-string.md) WIAで有効な文字に対してプロパティを設定\_DPS\_裏書き\_文字プロパティ。 ミニドライバーは、作成し、このプロパティを保持します。

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

[**WIA\_IP\_プリンター\_裏書き\_有効\_文字**](wia-ips-printer-endorser-valid-characters.md)

 

 






