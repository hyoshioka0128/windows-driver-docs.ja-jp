---
title: KSK プロパティ\_SYSAUDIO\_選択\_グラフ
description: KSK プロパティ\_SYSAUDIO\_SELECT\_GRAPH プロパティを使用して、仮想オーディオデバイス上のピンインスタンス用に SysAudio が構築するオプションのノードをグラフに明示的に含めます。
ms.assetid: 1107e20e-9ba8-4fda-8457-c357426a9cda
keywords:
- KSPROPERTY_SYSAUDIO_SELECT_GRAPH オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_SELECT_GRAPH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7d1a1fe5ea23ad96b54397bf4be0ac86916f71
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832719"
---
# <a name="ksproperty_sysaudio_select_graph"></a>KSK プロパティ\_SYSAUDIO\_選択\_グラフ


KSK プロパティ\_SYSAUDIO\_SELECT\_GRAPH プロパティを使用して、仮想オーディオデバイス上のピンインスタンス用に SysAudio が構築するオプションのノードをグラフに明示的に含めます。

## <span id="ddk_ksproperty_sysaudio_select_graph_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_SELECT_GRAPH_KS"></span>


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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph" data-raw-source="[&lt;strong&gt;SYSAUDIO_SELECT_GRAPH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph)"><strong>SYSAUDIO_SELECT_GRAPH</strong></a></p></td>
<td align="left"><p>なし</p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、SYSAUDIO\_型の構造であり、プロパティ、pin ID、およびノード ID を指定する\_グラフを選択します。 プロパティは、 [**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))型の埋め込み構造体によって指定されます。 Pin ID は、仮想オーディオデバイスをラップする KS フィルター内のピンファクトリを識別するインデックスです。 ノード ID は、指定されたピンのデータパスにあるオプションのノードを識別するインデックスです。 詳細については、次の「解説」を参照してください。

プロパティ値 (操作データ) がこのプロパティに対して定義されていません。 プロパティ値のバッファーポインターを**NULL**として指定し、そのサイズを0として指定します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

SYSAUDIO\_選択\_グラフプロパティ要求を選択する\_と、正常に完了したことを示す状態\_成功したことが示されます。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティは、通常、AEC ノードをピンインスタンスのグラフに強制的に配置するために使用されます。

仮想オーディオデバイスのフィルターでレンダリングピンをインスタンス化する場合、SysAudio はピンから開始され、既定ではフィルターを使用した最も単純なパスを表すグラフを選択します。 このグラフでは、AEC コントロールなどの任意のノードが除外されます。

Sysaudio の既定の動作をオーバーライドするには、まず sysaudio\_sysaudio AUDIO に送信し、グラフに含めるオプションのノードを指定する [\_グラフの設定-プロパティの要求] を選択します。 その後、SysAudio が pin インスタンスを作成すると、pin のグラフには、要求で指定されたオプションのノードが含まれます。

SYSAUDIO\_選択し\_グラフセット-property 要求\_は、要求の後に作成された pin インスタンスのみが影響を受けます。 要求は、以前にインスタンス化された pin には影響しません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**SYSAUDIO\_\_グラフの選択**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-sysaudio_select_graph)

[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

 

 






