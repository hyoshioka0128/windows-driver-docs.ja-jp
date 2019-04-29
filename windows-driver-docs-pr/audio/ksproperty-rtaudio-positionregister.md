---
title: KSPROPERTY\_RTAUDIO\_POSITIONREGISTER
description: KSPROPERTY\_RTAUDIO\_POSITIONREGISTER プロパティ、クライアントがアクセスできる仮想メモリの場所に特定のストリームをオーディオ デバイスの位置のレジスタにマップします。次の表では、このプロパティの機能をまとめたものです。
ms.assetid: 812072ec-d2a5-4e84-aebe-f24ca0d3cb21
keywords:
- KSPROPERTY_RTAUDIO_POSITIONREGISTER オーディオ デバイス
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
ms.openlocfilehash: fabefcd7ecaddb9efed29cf16c47b9fb6c2ff83e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332669"
---
# <a name="kspropertyrtaudiopositionregister"></a>KSPROPERTY\_RTAUDIO\_POSITIONREGISTER


KSPROPERTY\_RTAUDIO\_POSITIONREGISTER プロパティ、クライアントがアクセスできる仮想メモリの場所に特定のストリームをオーディオ デバイスの位置のレジスタにマップします。

次の表では、このプロパティの機能をまとめたものです。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537498" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537498)"><strong>KSRTAUDIO_HWREGISTER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537497" data-raw-source="[&lt;strong&gt;KSRTAUDIO_HWREGISTER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537497)"><strong>KSRTAUDIO_HWREGISTER</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンス データ) は、KSRTAUDIO\_HWREGISTER\_プロパティ構造体が含まれています、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体。 要求を送信する前に、クライアントは、登録の推奨されるベース アドレスを示す値を含む構造体を読み込みます。

プロパティの値 (データの操作) は、KSRTAUDIO\_プロパティ ハンドラーが、ハードウェア、マップが先の仮想アドレスを書き込む先 HWREGISTER 構造体はレジスタを配置します。 クライアントは、このアドレスから直接登録を読み取ることができます。 KSRTAUDIO\_HWREGISTER 構造では、速度を位置レジスタをインクリメント自体も指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_POSITIONREGISTER プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

通常、オーディオのアプリケーションは、オーディオ ストリームの現在の位置を監視する必要があります。 この位置はストリームの先頭からのバイト オフセットとして指定します。

-   レンダリングのストリームの場合は、ストリームの位置は、アナログ デジタル コンバーター (Dac) を使って現在再生されているオーディオ フレームのバイト オフセットは。

-   キャプチャのストリームの場合は、ストリームの位置は、アナログ/デジタル コンバーター (Adc) を使って現在記録中のオーディオのフレームのバイト オフセットは。

一部のオーディオ デバイスには、ストリームの実行中に継続的にインクリメントする位置のレジスタが含まれています。 1 つのチップにすべてのデジタルおよびアナログ関数が組み込まれているオーディオ デバイス、位置、レジスタ通常を示します、現在のストリームの位置直接。

ただし、バス コント ローラーとコーデックのチップを個別にデジタルおよびアナログ関数を分割するチップセット、位置、レジスタ バス コント ローラー チップでは一般にし、次のことを示します。

-   レンダリングのストリームの場合は、位置、レジスタは、バス コント ローラーは、コーデックを記述したオーディオ フレームの最後のバイト オフセットを示します。

-   キャプチャのストリームの場合は、位置、レジスタは、バス コント ローラーは、コーデックから読み取る直前のオーディオ フレームのバイト オフセットを示します。

どちらの場合も、位置レジスタの値では、コーデックを遅延は含まれません。 クライアントでは、コーデックの遅延を特定した場合は、(、Dac または ADCs) にある場合は true。 ストリームの位置を推定する位置のレジスタ値をこの遅延を追加できます。 照会することができます、コーデックから最悪の遅延を指定する CodecDelay 値の[ **KSPROPERTY\_RTAUDIO\_HWLATENCY** ](ksproperty-rtaudio-hwlatency.md)プロパティ。

成功した場合、KSPROPERTY\_RTAUDIO\_POSITIONREGISTER プロパティ要求位置の登録をユーザー モードまたはカーネル モード クライアントで指定したとおりのいずれかからクライアントにアクセスできる仮想メモリ アドレスにマップされます。 その後、クライアントは、現在の位置、レジスタの値を取得するには、このアドレスから読み取ります。

オーディオ ハードウェアでの仮想アドレスにマップできる位置登録がサポートされていない場合、プロパティの要求が失敗します。 この場合、クライアントがから位置を決定する必要があります、 [ **KSPROPERTY\_オーディオ\_位置**](ksproperty-audio-position.md)プロパティ。

Pin を閉じるときに、位置、レジスタのマッピングは破棄されます。 クライアントは、開かれた pin の有効期間内に 1 回だけ登録をマップでき、暗証番号 (pin) の位置の登録を再マップするための後続の呼び出しは失敗します。

通常は高速になります、KSPROPERTY を送信するよりも、位置、レジスタの読み取り\_オーディオ\_位置の要求は、ユーザー モードのクライアントのユーザー モードとカーネル モードの切り替えが必要です。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSRTAUDIO\_HWREGISTER**](https://msdn.microsoft.com/library/windows/hardware/ff537497)

[**KSRTAUDIO\_HWREGISTER\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff537498)

[**KSPROPERTY\_オーディオ\_位置**](ksproperty-audio-position.md)

[**KSPROPERTY\_RTAUDIO\_HWLATENCY**](ksproperty-rtaudio-hwlatency.md)

 

 






