---
title: KSPROPERTY\_SOUNDDETECTOR\_パターン
description: KSPROPERTY\_SOUNDDETECTOR\_パターン プロパティは、オペレーティング システムによって検出されたキーワードの構成に設定されています。
ms.assetid: 7A6AF4F6-5F5F-4A3D-AF61-B3E4374B33AD
keywords:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 981bdfcbc3308b459acea09d939548bc01288510
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391622"
---
# <a name="kspropertysounddetectorpatterns"></a>KSPROPERTY\_SOUNDDETECTOR\_パターン


**KSPROPERTY\_SOUNDDETECTOR\_パターン**を検出するキーワードを構成するオペレーティング システムで設定されます。

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
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>

 

OS をキーワード パターンを設定または空の値に設定可能性があります。

以前に装備された場合、OS は、このプロパティを設定、ドライバー、検出機能に自動的に disarms します。

ドライバーを使用して要求に失敗場合は、ドライバーは、リソース不足のための"set"要求を満たすことができない、**状態\_不十分\_リソース**します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティの値は、 [ **KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)構造体の後にアラインされた検出の 64 ビット パターンのシーケンス。 各パターンで始まる、 [ **SOUNDDETECTOR\_PATTERNHEADER** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sounddetector_patternheader)パターン ペイロードを続けています。

<a name="remarks"></a>注釈
-------

ドライバーはまで"set"要求を完了できません。

-   検出機能は解除とそれ以降の"get"要求[ **KSPROPERTY\_SOUNDDETECTOR\_故障**](ksproperty-sounddetector-armed.md) false を返します。
-   その後"get"要求[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT** ](ksproperty-sounddetector-matchresult.md)データは返されません。
-   キーワードの新しいパターンが確立されているし、新しいパターンで、キーワードの検出機能が動作しています。

ドライバーは、上記の条件が満たされるまで、保留中の要求を保持できます。 また、デバイスには、測定可能な初期化時間が必要とする場合、ドライバーを維持できます保留中のこの要求まで、デバイスが準備完了では、要求を処理します。

OS を回避するには、この動作が必要ですキーワードとキーワードのパターンを更新する間、検出された競合が条件 (例: キーワードが検出された場合と、KSEVENT\_SOUNDDETECTOR、OS の更新、キーワードの前に、インスタントが生成されます)。

OS は、2 秒以上でこの要求を完了するを待機します。

<a name="requirements"></a>必要条件
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
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**SOUNDDETECTOR\_PATTERNHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**SOUNDDETECTOR\_パターン**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn932155(v=vs.85))

[**KSPROPERTY\_SOUNDDETECTOR\_故障**](ksproperty-sounddetector-armed.md)

[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

 

 






