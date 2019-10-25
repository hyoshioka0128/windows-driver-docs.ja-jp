---
title: KSK プロパティ\_RTAUDIO\_BUFFER
description: KSK プロパティ\_RTAUDIO\_BUFFER プロパティは、ドライバーで割り当てられたオーディオデータ用の循環バッファーを指定します。次の表は、このプロパティの機能をまとめたものです。
ms.assetid: e2c78849-1a34-446c-9f44-012f36ddafa5
keywords:
- KSPROPERTY_RTAUDIO_BUFFER オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_BUFFER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c468124a7df73b79c443d7c4706e56767ef40ecf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830697"
---
# <a name="ksproperty_rtaudio_buffer"></a>KSK プロパティ\_RTAUDIO\_BUFFER


KSK プロパティ\_RTAUDIO\_BUFFER プロパティは、ドライバーで割り当てられたオーディオデータ用の循環バッファーを指定します。

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
<td align="left"><p><a href="ksrtaudio-buffer-property.md" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER_PROPERTY&lt;/strong&gt;](ksrtaudio-buffer-property.md)"><strong>KSRTAUDIO_BUFFER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)"><strong>KSRTAUDIO_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、他のメンバーと共に[**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体を含む KSRTAUDIO\_バッファー\_プロパティ構造で構成されます。 クライアントは、要求されたバッファーサイズを構造体に書き込みます。 クライアントが特定のベースアドレスを使用する必要がない場合は、ベースアドレスを**NULL**として指定する必要があります。

プロパティ値 (操作データ) は、KSRTAUDIO\_BUFFER 型の構造体です。 ドライバーは、この構造体に、割り当てられている循環バッファーの実際のバッファーサイズ、ベースアドレス、およびメモリバリアフラグを設定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_BUFFER property 要求\_は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。 次の表に、発生する可能性のあるエラー状態コードを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>指定されたバッファー属性の組み合わせを持つ循環バッファーを割り当てることができません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>バッファーのメモリを割り当てることができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>デバイスの準備ができていません</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ベースアドレスは、循環バッファーの開始時の仮想メモリアドレスです。 クライアントはこのアドレスでバッファーに直接アクセスできます。 バッファーは仮想メモリ内で連続しています。 バッファーを物理メモリ内で連続して使用するかどうかは、ドライバーによって決まります。

クライアントは、プロパティ記述子のベースアドレスを**NULL**に設定する必要があります。 ドライバーは、プロパティ値のベースアドレスを、割り当てられたオーディオバッファーの仮想アドレスに設定します。

通常、オーディオハードウェアでは、サンプル境界で開始および終了するために、またはハードウェアに依存する他のアラインメント制約を満たすために、オーディオバッファーを必要とします。 十分なメモリが使用可能な場合、最も近いサンプルまたはその他のハードウェアの制限付き境界に対して、要求されたサイズ (上または下) がバッファーの実際のサイズになります。 実際のサイズは、要求されたサイズ以上である必要があります。それ以外の場合、Audio Session API (オーバー API) オーディオエンジンはバッファーを使用せず、ストリームの作成は失敗します。

RTAUDIO\_バッファーのプロパティ要求が正常に\_場合、プロパティの値 (KSRTAUDIO\_BUFFER 型の構造) には、ドライバーによって割り当てられたバッファーのアドレスとサイズが含まれます。

Pin を閉じると、このプロパティを通じて割り当てられたバッファーが自動的に解放されます。

イベント通知が必要な場合は、ksk プロパティ\_RTAUDIO\_BUFFER ではなく[ **\_通知を使用して、Ksk プロパティ\_rtaudio\_buffer\_** ](ksproperty-rtaudio-buffer-with-notification.md)を呼び出す必要があります。

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


[**KSRTAUDIO\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)

[**KSRTAUDIO\_BUFFER\_プロパティ**](ksrtaudio-buffer-property.md)

[ **\_通知での RTAUDIO\_バッファー\_\_KSK プロパティ**](ksproperty-rtaudio-buffer-with-notification.md)

 

 






