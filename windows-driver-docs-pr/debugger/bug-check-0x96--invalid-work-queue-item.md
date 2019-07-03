---
title: バグ チェック 0x96 INVALID_WORK_QUEUE_ITEM
description: INVALID_WORK_QUEUE_ITEM のバグ チェックでは、0x00000096 の値を持ちます。 このバグ チェックでは、キューのエントリが NULL ポインターが含まれている削除されたことを示します。
ms.assetid: 18d7d8b2-814c-4207-aac9-e3affc2ccebd
keywords:
- バグ チェック 0x96 INVALID_WORK_QUEUE_ITEM
- INVALID_WORK_QUEUE_ITEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_WORK_QUEUE_ITEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 211cf83277a137f78bc1f0d0f5fe91d278c71a6e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519113"
---
# <a name="bug-check-0x96-invalidworkqueueitem"></a>バグ チェック 0x96:無効な\_作業\_キュー\_項目


無効な\_作業\_キュー\_項目のバグ チェックが 0x00000096 の値を持ちます。 このバグ チェックでは、キューのエントリが削除されたことを示すを含む、 **NULL**ポインター。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="invalidworkqueueitem-parameters"></a>無効な\_作業\_キュー\_アイテムのパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>キューのアドレスが<strong>flink</strong>または<strong>点滅</strong>フィールドは<strong>NULL</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>参照されるキューのアドレス。 通常、このキューは、 <strong>ExWorkerQueue</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>ベース アドレス、 <strong>ExWorkerQueue</strong>配列。 (このアドレスには、対象のキューが実際にはかどうかを決定するのに役立ちます、 <strong>ExWorkerQueue</strong>します。 キューの場合、 <strong>ExWorkerQueue</strong>、このパラメーターからのオフセットは、キューを分離します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>キューと仮定すると、 <strong>ExWorkerQueue</strong>、この値は、呼び出された場合は、作業項目を有効になっていたワーカー ルーチンのアドレス。 (このアドレスは作業キューが悪用するドライバーの分離を使用できます)。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

無効な\_作業\_キュー\_項目のバグ チェックが発生したときに**KeRemoveQueue**キュー エントリを削除しますが**flink**または**を点滅させる**フィールドは**NULL**します。

キューの誤用されてもこのエラーが発生します。 ワーカー スレッドの作業項目が誤って使用するため、通常このエラーが発生します。

キューのエントリは、1 回だけリストに挿入できます。 項目がキューから削除されたときにその**flink**にフィールドが設定されている**NULL**します。 次に、2 回目の項目が、このバグ チェックが行われます。

参照されているキューは、ほとんどの場合、 **ExWorkerQueue** (executive ワーカー キュー)。 エラーが発生したドライバーを識別できるように、パラメーター 4 には呼び出された場合、この作業項目を有効になっていたワーカー ルーチンのアドレスが表示されます。 ただしがの場合、キューが参照されているは、 **ExWorkerQueue**、このパラメーターは役に立ちません。

 

 




