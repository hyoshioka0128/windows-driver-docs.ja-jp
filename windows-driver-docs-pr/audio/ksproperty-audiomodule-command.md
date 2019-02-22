---
title: KSPROPERTY\_AUDIOMODULE\_コマンド
description: KSPROPERTY\_AUDIOMODULE\_コマンド プロパティは、コマンド プロパティを取得し、バッファーと指示 (暗証番号 (pin) のハンドル) のハードウェアまたはソフトウェアのキャッシュ (フィルター ハンドル) を設定するために使用します。
ms.assetid: 90C69481-A3DF-4801-8733-C417950880E5
keywords:
- KSPROPERTY_AUDIOMODULE_COMMAND オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_COMMAND
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52c6bf7350cd61659df8128986067d5d04029dfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551692"
---
# <a name="kspropertyaudiomodulecommand"></a>KSPROPERTY\_AUDIOMODULE\_コマンド


**KSPROPERTY\_AUDIOMODULE\_コマンド**プロパティは、コマンドのプロパティを取得し、バッファーと指示 (暗証番号 (pin) のハンドル) のハードウェアまたはソフトウェアのキャッシュ (フィルター ハンドル) を設定するために使用します。

*設定*値は、コマンドの一部として提供されます。 ときに、*取得*が使用すると、このコマンドの結果を返します。

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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルターまたはピン留めします。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt808139" data-raw-source="[&lt;strong&gt;KSAUDIOMODULE_PROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt808139)"><strong>KSAUDIOMODULE_PROPERTY</strong> </a> + [省略可能なカスタム モジュールの引数]</p></td>
<td align="left"><p>未定義</p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型は、定義されていません。 実装者は、モジュールの特定のカスタム コマンドの構造を作成できます。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOMODULE\_コマンド**オーディオ モジュールのコマンド固有の情報を返します。

<a name="remarks"></a>注釈
-------

サポート、 **KSPROPERTY\_AUDIOMODULE\_コマンド**プロパティは、クエリを実行して、オーディオのモジュールのパラメーターを設定するカスタム コマンドを送信するオーディオ モジュールのクライアントを使用します。 プロパティは、フィルターまたは暗証番号 (pin) のハンドルを使用して送信できる、 [ **KSAUDIOMODULE\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/mt808139) DeviceIoControl の呼び出しの入力バッファーとして渡されます。 クライアントできます必要に応じて追加情報を送信する隣接、 **KSAUDIOMODULE\_プロパティ**カスタム コマンドを送信する入力バッファーにします。

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

 

 






