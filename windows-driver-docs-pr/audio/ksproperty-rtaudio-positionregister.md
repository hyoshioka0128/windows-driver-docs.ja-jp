---
title: KSK プロパティ\_RTAUDIO\_POSITIONREGISTER
description: KSK プロパティ\_RTAUDIO\_POSITIONREGISTER プロパティは、特定のストリームのオーディオデバイスの位置登録をクライアントがアクセスできる仮想メモリ位置にマップします。次の表は、このプロパティの機能をまとめたものです。
ms.assetid: 812072ec-d2a5-4e84-aebe-f24ca0d3cb21
keywords:
- KSPROPERTY_RTAUDIO_POSITIONREGISTER オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_POSITIONREGISTER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8095b94a315c2443800ed8600df65b6369223717
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830643"
---
# <a name="ksproperty_rtaudio_positionregister"></a>KSK プロパティ\_RTAUDIO\_POSITIONREGISTER


KSK プロパティ\_RTAUDIO\_POSITIONREGISTER プロパティは、特定のストリームのオーディオデバイスの位置登録をクライアントがアクセスできる仮想メモリ位置にマップします。

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

 

プロパティ記述子 (インスタンスデータ)\_は、HWREGISTER\_プロパティ構造体であり、 [**Ksproperty**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造を格納しています。 クライアントは、要求を送信する前に、レジスタの優先ベースアドレスを示す値を使用して構造体を読み込みます。

プロパティ値 (操作データ) は、KSRTAUDIO\_HWREGISTER 構造体です。この構造体は、ハードウェアの位置登録がマップされている仮想アドレスをプロパティハンドラーが書き込みます。 クライアントは、このアドレスから登録を直接読み取ることができます。 KSRTAUDIO\_HWREGISTER 構造体は、位置レジスタがそれ自体をインクリメントする速度も指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_POSITIONREGISTER property 要求\_は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

通常、オーディオアプリケーションでは、オーディオストリームの現在位置を監視する必要があります。 この位置は、ストリームの先頭からのバイトオフセットとして指定されます。

-   レンダリングストリームの場合、ストリームの位置は、デジタル-アナログコンバーター (Dac) を通じて現在再生されているオーディオフレームのバイトオフセットです。

-   キャプチャストリームの場合、ストリームの位置は、現在アナログ-デジタルコンバーター (ADCs) を介して記録されているオーディオフレームのバイトオフセットです。

一部のオーディオデバイスには、ストリームの実行中に継続的に増加する位置レジスタが含まれています。 すべてのデジタルおよびアナログの機能が1つのチップに組み込まれているオーディオデバイスでは、通常、位置登録は現在のストリームの位置を直接示します。

ただし、デジタルおよびアナログ機能を別個のバスコントローラーとコーデックチップに分割するチップセットの場合、通常、位置登録はバスコントローラーチップに配置され、次のことが示されます。

-   レンダリングストリームの場合、位置レジスタは、バスコントローラーがコーデックに書き込んだ最後のオーディオフレームのバイトオフセットを示します。

-   キャプチャストリームの場合、位置レジスタは、バスコントローラーがコーデックから読み取った最後のオーディオフレームのバイトオフセットを示します。

どちらの場合も、位置レジスタの値にはコーデックの遅延が含まれません。 クライアントがコーデックの遅延を決定した場合、この遅延を位置レジスタの値に追加して、実際のストリームの位置 (Dac または ADCs) を推定することができます。 コーデックを使用した最悪の遅延を指定する CodecDelay 値の場合は、 [**RTAUDIO\_HWLATENCY プロパティ\_** ](ksproperty-rtaudio-hwlatency.md)にクエリを実行できます。

正常に実行された場合、RTAUDIO\_POSITIONREGISTER プロパティ要求で\_は、クライアントが指定したとおりに、ユーザーモードまたはカーネルモードからクライアントにアクセスできる仮想メモリアドレスに位置レジスタがマップされます。 その後、クライアントはこのアドレスから読み取り、位置レジスタの現在の値を取得します。

オーディオハードウェアが、仮想アドレスにマップできる位置登録をサポートしていない場合、プロパティ要求は失敗します。 この場合、クライアントは、 [**Ksk プロパティ\_AUDIO\_position**](ksproperty-audio-position.md)プロパティからの位置を決定する必要があります。

位置レジスタのマッピングは、ピンが閉じたときに破棄されます。 クライアントは、開いている pin の有効期間中に1回だけレジスタをマップできます。また、pin の位置レジスタを再マップするための後続の呼び出しは失敗します。

通常、位置レジスタは、KSK プロパティ\_AUDIO\_POSITION 要求を送信するよりも高速です。この場合、ユーザーモードのクライアントではユーザーモードとカーネルモードの間の移行が必要になります。

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO\_HWREGISTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister)

[**KSRTAUDIO\_HWREGISTER\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_hwregister_property)

[**KSK プロパティ\_オーディオ\_位置**](ksproperty-audio-position.md)

[**KSK プロパティ\_RTAUDIO\_HWLATENCY**](ksproperty-rtaudio-hwlatency.md)

 

 






