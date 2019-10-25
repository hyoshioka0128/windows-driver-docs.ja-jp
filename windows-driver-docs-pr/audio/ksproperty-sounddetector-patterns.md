---
title: KSK プロパティ\_SOUNDDETECTOR\_パターン
description: '\_SOUNDDETECTOR\_PATTERNS プロパティは、検出されるキーワードを構成するためにオペレーティングシステムによって設定されます。'
ms.assetid: 7A6AF4F6-5F5F-4A3D-AF61-B3E4374B33AD
keywords:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_PATTERNS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 35ef2ecc1fde4511ef186746c35fc0c744a5a0fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830580"
---
# <a name="ksproperty_sounddetector_patterns"></a>KSK プロパティ\_SOUNDDETECTOR\_パターン

**\_sounddetector\_PATTERNS**プロパティは、検出されるキーワードを構成するためにオペレーティングシステムによって設定されます。

OS はキーワードパターンを設定するか、これを空の値に設定することができます。

OS がこのプロパティを設定すると、ドライバーは以前に検出された検出を自動的に無効にします。

リソース不足のためにドライバーが "set" 要求を満たすことができない場合、ドライバーは要求に失敗し、**リソース\_不足**している\_状態になります。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル-KSPROPSETID_SoundDetector

この使用状況テーブルでは、 [KSPROPSETID_SoundDetector](kspropsetid-sounddetector.md)を使用して\_\_の KSPROPERTY に sounddetector 器が呼び出されるタイミングをまとめます。

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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table---kspropsetid_sounddetector2"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル-KSPROPSETID_SoundDetector2

この使用状況テーブルでは、 [KSPROPSETID_SoundDetector2](kspropsetid-sounddetector2.md)を使用して\_\_の KSPROPERTY に sounddetector 器が呼び出されるタイミングをまとめます。

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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)"><strong>KSMULTIPLE_ITEM</strong></a></p></td>
</tr>
</tbody>
</table>


### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティ値は、 [**Ksmultiple\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)構造体の後に、一連の64ビットアラインされた検出パターンが続きます。 各パターンは、[**サウンド検出機能\_PATTERN ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)の後にパターンペイロードが続きます。

<a name="remarks"></a>注釈
-------

ドライバーは、次のようになるまで "設定" 要求を完了できません。

-   検出が無効になり、それ以降の[**Ksk プロパティ\_** ](ksproperty-sounddetector-armed.md)の "get" 要求が発生しても、\_は false を返します。
-   次に、Ksk プロパティに対する "get" 要求[ **\_SOUNDDETECTOR\_MATCHRESULT**](ksproperty-sounddetector-matchresult.md)はデータを返しません。
-   新しいキーワードパターンが確立され、キーワード検出機能が新しいパターンで動作しています。

ドライバーは、上記の条件が満たされるまで要求を保留状態のままにすることができます。 また、デバイスで測定可能な初期化時間が必要な場合、デバイスの準備が完了し、が要求を処理できるようになるまで、ドライバーはこの要求を保留状態のままにすることができます。

OS はこの動作を必要とします。検出されたキーワードとキーワードパターンを更新したときの競合状態を回避します (たとえば、キーワードが検出され、OS がキーワードを更新する前に KSEVENT\_SOUNDDETECTOR が生成された場合など)。

OS は、この要求が完了するまで少なくとも2秒間待機します。

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
<td align="left"><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**SOUNDDETECTOR\_PATTERN ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sounddetector_patternheader)

[**サウンド検出機能\_パターン**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn932155(v=vs.85))

[**KSK プロパティ\_SOUNDDETECTOR\_** ](ksproperty-sounddetector-armed.md)

[ **\_MATCHRESULT の KSK プロパティ\_SOUNDDETECTOR**](ksproperty-sounddetector-matchresult.md)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






