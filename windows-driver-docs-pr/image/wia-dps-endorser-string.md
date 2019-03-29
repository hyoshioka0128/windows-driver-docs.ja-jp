---
title: WIA\_DPS\_裏書き\_文字列
description: WIA\_DPS\_裏書き\_文字列プロパティには、ミニドライバーをスキャンする各ページの (つまり、印刷物) が承認されるは文字列が含まれています。
ms.assetid: c51a2941-9101-4749-8fa7-b9f3bbcb0803
keywords:
- WIA_DPS_ENDORSER_STRING イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_ENDORSER_STRING
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0df4751804fe5054ccff7c6707ed3fdda124480
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579661"
---
# <a name="wiadpsendorserstring"></a>WIA\_DPS\_裏書き\_文字列


WIA\_DPS\_裏書き\_文字列プロパティには、ミニドライバーをスキャンする各ページの (つまり、印刷物) が承認されるは文字列が含まれています。

## <span id="ddk_wia_dps_endorser_string_si"></span><span id="DDK_WIA_DPS_ENDORSER_STRING_SI"></span>


**注**  このプロパティは廃止されました。 使用[ **WIA\_IP\_プリンター\_裏書き\_文字列**](wia-ips-printer-endorser-string.md)代わりにします。

 

プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

アプリケーション設定、WIA\_DPS\_裏書き\_で報告される文字列のプロパティ設定が有効な文字を使用して、 [ **WIA\_DPS\_裏書き\_文字**](wia-dps-endorser-characters.md)プロパティ。 WIA で文字列が設定されている場合にのみ、WIA ミニドライバーはドキュメントを保証する必要があります\_DPS\_裏書き\_文字列。 空の文字列では、裏書き機能が無効になっていることを意味します。

ドライバーが WIA で特殊文字を使用できます、ドライバーは、裏書き文字列を解釈する必要があります、ため、\_DPS\_裏書き\_文字列。 ただし、アプリケーションのみがこれらの文字を理解できます。

WIA をサポートしているドライバー\_DPS\_裏書き\_文字列プロパティは、次のトークンの一覧をサポートする必要があります。

<span id="_DATE__"></span><span id="_date__"></span>$DATE $   
ローカル形式 YYYY/の形式で日付

<span id="_DAY__"></span><span id="_day__"></span>$DAY $   
1 日に、フォーム DD.

<span id="_MONTH__"></span><span id="_month__"></span>$MONTH $   
年、MM、フォームの月です。

<span id="_PAGE_COUNT__"></span><span id="_page_count__"></span>$PAGE\_カウント $   
転送されるページ数。

<span id="_TIME__"></span><span id="_time__"></span>$TIME $   
1 日に、HH:MM:SS の形式の時刻。

<span id="_YEAR__"></span><span id="_year__"></span>$YEAR$ $   
年 (YYYY の形式で)。

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


[**WIA\_DPS\_裏書き\_文字**](wia-dps-endorser-characters.md)

[**WIA\_IP\_プリンター\_裏書き\_文字列**](wia-ips-printer-endorser-string.md)

 

 






