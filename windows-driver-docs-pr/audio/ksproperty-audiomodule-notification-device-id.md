---
title: KSK プロパティ\_AUDIOMODULE\_NOTIFICATION\_デバイス\_ID
description: KSK プロパティ\_AUDIOMODULE\_NOTIFICATION\_デバイス\_ID は、オーディオモジュール通知デバイス識別子の GUID を取得します。
ms.assetid: CD9C5FCD-FB2A-4B21-A15E-BA520C3311A7
keywords:
- KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_NOTIFICATION_DEVICE_ID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 445d17f5adbce2bd0da77d4b398a0b7b57497678
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832843"
---
# <a name="ksproperty_audiomodule_notification_device_id"></a>KSK プロパティ\_AUDIOMODULE\_NOTIFICATION\_デバイス\_ID


**Ksk プロパティ\_audiomodule\_notification\_デバイス\_ID**は、オーディオモジュール通知デバイス識別子の GUID を取得します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>フィルターハンドルまたはピンハンドル</p></td>
<td align="left"><p>KSPROPERTY</p></td>
<td align="left"><p>GUID</p></td>
</tr>
</tbody>
</table>

 

返されるプロパティ値は単一の GUID です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_audiomodule\_notification\_デバイス\_ID**は、オーディオモジュール通知デバイス識別子に関連付けられた GUID を返します。

フィルターハンドルまたはピンハンドルがターゲットとして指定されている場合、同じデバイス GUID 値が返されます。

<a name="remarks"></a>注釈
-------

ミニポートが通知を通知し、オーディオモジュールクライアントに情報を渡すことができるようにするには、KSK プロパティ\_AUDIOMODULE\_NOTIFICATION\_デバイス\_ID が必要です。 この ID の有効期間は、オーディオデバイスが公開され、Windows オーディオスタックに対してアクティブになっている有効期間に関連付けられています。 プロパティは、フィルターまたはピンハンドルを介して送信できます。また、DeviceIoControl 呼び出しの入力バッファーとして KSK プロパティが渡されます。

この KSK プロパティの使用例については、SYSVAD audio driver サンプルを参照してください。

オーディオモジュールの詳細については、「[オーディオモジュール検出の実装](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)」を参照してください。

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
<td align="left"><p>Windows 10 バージョン1703</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[KSPROPSETID\_AudioModule](kspropsetid-audiomodule.md)

[**KSAUDIOMODULE\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_notification)

 

 






