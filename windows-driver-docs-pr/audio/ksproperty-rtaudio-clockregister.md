---
title: KSPROPERTY\_RTAUDIO\_CLOCKREGISTER
description: KSPROPERTY\_RTAUDIO\_CLOCKREGISTER プロパティは、クライアントがアクセスできる仮想メモリの場所にオーディオ デバイスのウォール クロック レジスタをマップします。 次の表では、このプロパティの機能をまとめたものです。
ms.assetid: a35b5830-55e4-4e92-a4f1-df9edcc2f5bb
keywords:
- KSPROPERTY_RTAUDIO_CLOCKREGISTER オーディオ デバイス
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
ms.openlocfilehash: 32b22c090abbb36dda353946fb2360044a6928b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332678"
---
# <a name="kspropertyrtaudioclockregister"></a>KSPROPERTY\_RTAUDIO\_CLOCKREGISTER


KSPROPERTY\_RTAUDIO\_CLOCKREGISTER プロパティは、クライアントがアクセスできる仮想メモリの場所にオーディオ デバイスのウォール クロック レジスタをマップします。

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

 

プロパティ記述子 (インスタンス データ) から成る、KSRTAUDIO\_HWREGISTER\_プロパティ構造を含む、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造体。 要求を送信する前にクライアントの読み込み、KSRTAUDIO\_HWREGISTER\_クロック登録の推奨されるベース アドレスを示す値を持つプロパティ構造体。

プロパティの値 (データの操作) は、KSRTAUDIO へのポインター\_HWREGISTER 構造体のレジスタのアドレスと登録更新頻度をプロパティ ハンドラーを書き込みます。 この登録アドレスは、ハードウェア レジスタのマップ先のユーザー モードまたはカーネル モード仮想アドレスです。 クライアントは、このアドレスから直接登録を読み取ることができます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_RTAUDIO\_CLOCKREGISTER プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は失敗を示すエラー コードを返します。

<a name="remarks"></a>注釈
-------

一部のオーディオ デバイスには、クロックのレジスタが含まれています。 クロックの登録は、ハードウェアの電源が入るし、ハードウェアの電源と停止の実行を開始するウォール クロック カウンターです。 ソフトウェアは、デバイスのハードウェア クロックの間の相対的な誤差を測定することで、2 つまたは複数のコント ローラー デバイス間で同期する時計のレジスタを使用します。

成功した場合、プロパティの要求はクロックの登録をユーザー モードまたはカーネル モード クライアントで指定したとおりのいずれかからアクセスできる仮想メモリ アドレスにマップします。 その後、クライアントは、クロックのレジスタの現在の値を取得するには、このアドレスから読み取ります。

オーディオ ハードウェアは仮想メモリをマップできるクロック登録をサポートしていない場合、プロパティの要求が失敗します。

クロック レジスタのマッピングは、暗証番号 (pin) の終了時に破棄されます。 クライアントは、暗証番号 (pin) のインスタンスの有効期間中に 1 回だけ登録をマップでき、そのインスタンス用にもう一度クロック レジスタにマップする任意の後続の呼び出しは失敗します。

これは通常高速化を送信するよりも、クロックの登録を読み取る、 [ **KSPROPERTY\_クロック\_時間**](https://msdn.microsoft.com/library/windows/hardware/ff565095)要求は、ユーザー モードとカーネル モードの間の遷移が必要ですユーザー モードのクライアントです。

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
<td align="left"><p>Windows Vista 以降の Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSRTAUDIO\_HWREGISTER\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff537498)

[**KSRTAUDIO\_HWREGISTER**](https://msdn.microsoft.com/library/windows/hardware/ff537497)

 

 






