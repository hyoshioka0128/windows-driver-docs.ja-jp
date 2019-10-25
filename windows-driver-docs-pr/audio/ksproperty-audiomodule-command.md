---
title: KSK プロパティ\_AUDIOMODULE\_コマンド
description: KSK プロパティ\_AUDIOMODULE\_コマンドプロパティは、ハードウェア (ピンハンドル) またはソフトウェアキャッシュ (フィルターハンドル) のバッファーと命令を取得および設定するために使用されるコマンドプロパティです。
ms.assetid: 90C69481-A3DF-4801-8733-C417950880E5
keywords:
- KSPROPERTY_AUDIOMODULE_COMMAND オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOMODULE_COMMAND
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1626793bee02a406cc062e0a3b1b9e5c376403e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832865"
---
# <a name="ksproperty_audiomodule_command"></a>KSK プロパティ\_AUDIOMODULE\_コマンド


**Ksk プロパティ\_AUDIOMODULE\_コマンド**プロパティは、ハードウェア (ピンハンドル) またはソフトウェアキャッシュ (フィルターハンドル) のバッファーと命令を取得および設定するために使用されるコマンドプロパティです。

*設定*値は、コマンドの一部として提供されます。 *Get*を使用すると、このコマンドの結果が返されます。

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
<td align="left"><p>フィルターまたはピン留め</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property" data-raw-source="[&lt;strong&gt;KSAUDIOMODULE_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)"><strong>KSAUDIOMODULE_PROPERTY</strong></a> + [省略可能なカスタムモジュール引数]</p></td>
<td align="left"><p>シンボル</p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型が未定義です。 実装者は、モジュール固有のカスタムコマンド構造を作成できます。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ\_audiomodule\_command**は、オーディオモジュールコマンド固有の情報を返します。

<a name="remarks"></a>注釈
-------

**Ksk プロパティ\_audiomodule\_COMMAND**プロパティのサポートにより、オーディオモジュールクライアントは、オーディオモジュールのクエリおよび設定パラメーターにカスタムコマンドを送信できます。 プロパティは、フィルターまたはピンハンドルを介して送信できます。また、 [**KSAUDIOMODULE\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudiomodule_property)は、DeviceIoControl 呼び出しの入力バッファーとして渡されます。 クライアントは、必要に応じて、入力バッファーの**KSAUDIOMODULE\_プロパティ**に隣接する追加情報を送信して、カスタムコマンドを送信できます。

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

 

 






