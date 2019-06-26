---
title: KSPROPERTY\_RTAUDIO\_クエリ\_通知\_サポート
description: クライアント アプリケーションが使用、KSPROPERTY\_RTAUDIO\_クエリ\_通知\_オーディオ ドライバーをプロセスが実行されるときにクライアント アプリケーションに通知するかどうかを決定するプロパティをサポートします送信バッファーが完了しました。
ms.assetid: 7e0910df-4b76-4e61-9f88-8953860f3abe
keywords:
- KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0bec65c2f7eb92fe4c8b1533828eba302cdbe1d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391652"
---
# <a name="kspropertyrtaudioquerynotificationsupport"></a>KSPROPERTY\_RTAUDIO\_クエリ\_通知\_サポート


クライアント アプリケーションを使用して、`KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT`オーディオ ドライバーがプロセスで送信されたバッファーで実行されるときに、クライアント アプリケーションを通知するかどうかを確認するには完了します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は、BOOL 型の変数です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

応答を`KSPROPERTY_RTAUDIO_QUERY_NOTIFICATION_SUPPORT`ドライバーは、要求のプロパティを返します、 **TRUE**または**FALSE**値。 この値は、ドライバーが、プロパティをサポートするかどうかによって異なります。

<a name="remarks"></a>注釈
-------

なし

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






