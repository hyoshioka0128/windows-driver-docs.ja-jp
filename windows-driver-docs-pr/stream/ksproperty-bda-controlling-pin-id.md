---
title: KSPROPERTY\_BDA\_制御\_PIN\_ID
description: クライアントを使用して、KSPROPERTY\_BDA\_制御\_PIN\_BDA テンプレートの接続リスト内のノードの制御の暗証番号 (pin) を取得する ID。
ms.assetid: d40454a3-0938-4efb-8b06-06b599be8b20
keywords:
- KSPROPERTY_BDA_CONTROLLING_PIN_ID ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CONTROLLING_PIN_ID
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cd00b01a3e598d48cc98e2924e20201a9ecc4f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529903"
---
# <a name="kspropertybdacontrollingpinid"></a>KSPROPERTY\_BDA\_制御\_PIN\_ID


クライアントを使用して、KSPROPERTY\_BDA\_制御\_PIN\_BDA テンプレートの接続リスト内のノードの制御の暗証番号 (pin) を取得する ID。

## <span id="ddk_ksproperty_bda_controlling_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_CONTROLLING_PIN_ID_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p>KSP_BDA_NODE_PIN</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

戻り値は、制御の暗証番号 (pin) の ID を指定します。

ノードは、フィルター、入力ピンまたは出力ピンのいずれかで 1 つの pin に関連付けられます。 ノードには、独自のファイル ハンドルがあるないために、ノードはのみ制御の暗証番号 (pin) を介してアクセスできます。 このプロパティは、KSP ネットワーク プロバイダーを使用して\_BDA\_ノード\_BDA テンプレートの接続リスト内の各ノードの制御の暗証番号 (pin) のクエリをピン留めする構造体 (KSTOPOLOGY\_接続または BDA\_テンプレート\_接続配列)。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyGetControllingPinId**](https://msdn.microsoft.com/library/windows/hardware/ff556480)

[**BDA\_テンプレート\_接続**](https://msdn.microsoft.com/library/windows/hardware/ff556558)

[**KSP\_BDA\_ノード\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566716)

[**KSTOPOLOGY\_接続**](https://msdn.microsoft.com/library/windows/hardware/ff567148)

 

 






