---
title: KSPROPERTY\_オーディオ\_フィルター\_状態
description: KSPROPERTY\_オーディオ\_フィルター\_状態プロパティを使用して、プロパティの一覧のセットをサポートしている GFX フィルターのクエリを実行します。 一覧は、プロパティ セット Guid の配列の形式で取得されます。
ms.assetid: e0a3bce7-d321-445c-866c-78502b5ea887
keywords:
- KSPROPERTY_AUDIO_FILTER_STATE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_FILTER_STATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11f4dfcd79e4206bdaa55b569a6df7fd2f7999b0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532137"
---
# <a name="kspropertyaudiofilterstate"></a>KSPROPERTY\_オーディオ\_フィルター\_状態


KSPROPERTY\_オーディオ\_フィルター\_状態プロパティを使用して、プロパティの一覧のセットをサポートしている GFX フィルターのクエリを実行します。 一覧は、プロパティ セット Guid の配列の形式で取得されます。

## <span id="ddk_ksproperty_audio_filter_state_ks"></span><span id="DDK_KSPROPERTY_AUDIO_FILTER_STATE_KS"></span>


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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>Guid の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティのデータ (データの操作) は、Guid の配列です。 配列内の各 GUID は、フィルターをサポートしているプロパティの設定を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_フィルター\_プロパティ要求の状態が状態を返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

このプロパティを表す Guid の配列のサイズは、フィルターをサポートするプロパティ セットの数によって異なります。 配列を取得する前にクライアント最初に照会するプロパティの GUID の配列のサイズ、KSPROPERTY ミニポート ドライバーのプロパティのハンドラーを送信することによって\_オーディオ\_フィルター\_長さ 0 のプロパティの get 要求の状態プロパティ値のバッファー。 ハンドラーが必要なバッファー サイズと状態コードの状態を返すことによって応答\_バッファー\_オーバーフローが発生します。 詳細については、[オーディオ プロパティ ハンドラー](https://msdn.microsoft.com/library/windows/hardware/ff536214)を参照してください。

KSPROPERTY から Guid の配列を持つ\_オーディオ\_フィルター\_状態プロパティ get 要求と、オペレーティング システムは、各プロパティ セット内のプロパティを問い合わせること逐次的に。 この情報は、オペレーティング システム、フィルターをインスタンス化時に GFX フィルター オブジェクトの状態を復元し、フィルターが破棄される時点で GFX フィルター オブジェクトの状態を保存できます。 オペレーティング システムにその要求の各プロパティ セット内のプロパティがシリアル化」の説明に従って保存または GFX フィルターの状態を復元する、 [KS プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff567671)します。 保存と GFX フィルターの状態の復元の目的は、フィルターの設定、ユーザーが行った変更を保持するために、フィルターの連続するインスタンスの間で永続的な設定を行うことです。 .

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






