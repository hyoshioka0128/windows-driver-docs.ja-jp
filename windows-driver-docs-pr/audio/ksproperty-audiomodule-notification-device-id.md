---
title: KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID
description: KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID オーディオ モジュールの通知のデバイス id の GUID を取得します。
ms.assetid: CD9C5FCD-FB2A-4B21-A15E-BA520C3311A7
keywords:
- KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1409f8a7e6f64a4c239b87aca0c0a0b6dadabacf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332797"
---
# <a name="kspropertyaudiomodulenotificationdeviceid"></a>KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID


**KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID**オーディオ モジュールの通知のデバイス id の GUID を取得します。

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
<td align="left"><p>フィルターのハンドルまたは暗証番号 (pin) のハンドル</p></td>
<td align="left"><p>KSPROPERTY</p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

返されたプロパティの値は、1 つの GUID です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID**オーディオ モジュール通知デバイスの id に関連付けられた GUID を返します。

フィルターのハンドルまたは暗証番号 (pin) のハンドルが、ターゲットとして指定されている場合は、同じデバイス GUID 値が返されます。

<a name="remarks"></a>コメント
-------

サポート、KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ミニポート シグナル通知を有効にして、オーディオのモジュールのクライアントに情報を渡すに ID が必要です。 この ID の有効期間が公開されていると、Windows オーディオ スタックをアクティブにされているオーディオ デバイスの有効期間に関連付けられています。 フィルターまたは暗証番号 (pin) のハンドルを使用して、プロパティを送信することができます、KSPROPERTY が DeviceIoControl の呼び出しの入力バッファーとして渡されます。

この KSPROPERTY を使用する例は、SYSVAD オーディオ ドライバーのサンプルを参照してください。

オーディオのモジュールの詳細については、次を参照してください。[オーディオ モジュールの検出を実装する](https://msdn.microsoft.com/windows/hardware/drivers/audio/implementing-audio-module-communication)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>サポートなし</p></td>
</tr>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 バージョン 1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

[**KSAUDIOMODULE\_通知**](https://msdn.microsoft.com/library/windows/hardware/mt808138)

 

 






