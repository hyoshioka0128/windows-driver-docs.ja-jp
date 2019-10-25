---
title: KSK プロパティ\_RTAUDIO\_CLOCKREGISTER
description: KSK プロパティ\_RTAUDIO\_CLOCKREGISTER プロパティは、オーディオデバイスのウォールクロックレジスタを、クライアントがアクセスできる仮想メモリの場所にマップします。 次の表は、このプロパティの機能をまとめたものです。
ms.assetid: a35b5830-55e4-4e92-a4f1-df9edcc2f5bb
keywords:
- KSPROPERTY_RTAUDIO_CLOCKREGISTER オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_CLOCKREGISTER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2ba4b7123e379980e0bf9eea964fee21fe24afc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830679"
---
# <a name="ksproperty_rtaudio_clockregister"></a>KSK プロパティ\_RTAUDIO\_CLOCKREGISTER


KSK プロパティ\_RTAUDIO\_CLOCKREGISTER プロパティは、オーディオデバイスのウォールクロックレジスタを、クライアントがアクセスできる仮想メモリの場所にマップします。

次の表は、このプロパティの機能をまとめたものです。

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)"><strong>KSRTAUDIO_HWREGISTER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister)"><strong>KSRTAUDIO_HWREGISTER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、\_の[**プロパティ構造を**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))含む KSRTAUDIO\_HWREGISTER のプロパティ構造で構成されます。 クライアントは、要求を送信する前に、KSRTAUDIO\_HWREGISTER\_プロパティ構造体を、クロックレジスタの優先ベースアドレスを示す値と共に読み込みます。

プロパティ値 (操作データ) は、KSRTAUDIO\_HWREGISTER 構造体へのポインターであり、プロパティハンドラーによってレジスタアドレスとレジスタ更新頻度が書き込まれます。 この登録アドレスは、ハードウェアレジスタがマップされるユーザーモードまたはカーネルモードの仮想アドレスです。 クライアントは、このアドレスから登録を直接読み取ることができます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_CLOCKREGISTER property 要求\_は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求はエラーを示すエラーコードを返します。

<a name="remarks"></a>注釈
-------

一部のオーディオデバイスには、クロックレジスタが含まれています。 クロックレジスタは、ハードウェアの電源がオンになったときに実行を開始し、ハードウェアの電源が切れたときに停止するウォールクロックカウンターです。 ソフトウェアは、クロックレジスタを使用して、デバイスのハードウェアクロック間の相対的なずれを測定することで、2つ以上のコントローラーデバイス間で同期を行います。

成功した場合、プロパティ要求は、クライアントによって指定されたユーザーモードまたはカーネルモードからアクセスできる仮想メモリアドレスに、クロックレジスタをマップします。 その後、クライアントはこのアドレスから読み取り、クロックレジスタの現在の値を取得します。

オーディオハードウェアで、仮想メモリにマップできるクロックレジスタがサポートされていない場合、プロパティ要求は失敗します。

Pin を閉じると、クロックレジスタのマッピングが破棄されます。 クライアントは、pin インスタンスの有効期間内に1回だけレジスタをマップできます。それ以降の呼び出しでは、そのインスタンスに対して、時計レジスタが再度マップされます。

通常、クロックレジスタを読み取る方が、 [**Ksk プロパティ\_clock\_TIME**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-clock-time)要求を送信するよりも高速です。この場合、ユーザーモードのクライアントに対してユーザーモードとカーネルモードの間の移行が必要になります。

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
<td align="left"><p>Windows Vista 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSRTAUDIO\_HWREGISTER\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)

[**KSRTAUDIO\_HWREGISTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister)

 

 






