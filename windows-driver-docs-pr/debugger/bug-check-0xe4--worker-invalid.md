---
title: バグ チェック 0xE4 WORKER_INVALID
description: WORKER_INVALID のバグ チェックでは、0x000000E4 の値を持ちます。 これは通常、役員を含めることはできませんが、そのメモリを示します作業項目には、このような項目にが含まれています。
ms.assetid: 93951b77-bedf-4781-9c2b-e8df2aa8cb1c
keywords:
- バグ チェック 0xE4 WORKER_INVALID
- WORKER_INVALID
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WORKER_INVALID
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e4b621d134d4086c8d511f4c1cd853f0b69b98e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559693"
---
# <a name="bug-check-0xe4-workerinvalid"></a>バグ チェック 0xE4 の。ワーカー\_が無効です


ワーカー\_の無効なバグ チェックが 0x000000E4 の値を持ちます。 これは、そのメモリを含めることはできません、executive の作業項目は、このような項目は含ままたは現在アクティブな作業項目がキューに入れられたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="workerinvalid-parameters"></a>ワーカー\_パラメーターが無効です


パラメーター 1 では、コードの位置を示します。

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
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>プールのブロックの開始</p></td>
<td align="left"><p>プールのブロックの終了</p></td>
<td align="left"><p>アクティブなワーカーの項目が解放されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>キューの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>アクティブなワーカーの項目がキューに登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>I/O ワーカー ルーチンのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>キューに置かれた I/O ワーカー項目が解放されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>無効なオブジェクトのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効なオブジェクトを持つ I/O ワーカー項目を初期化しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>キューの数</p></td>
<td align="left"><p>対象とする NUMA ノードまたはすべてのノードが検索された場合は-1。</p></td>
<td align="left"><p>ワーカーがキューに登録が初期化される前に、作業項目をキューに試行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>キューの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効なキューの種類が指定されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>作業項目のアドレス</p></td>
<td align="left"><p>キューの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>無効なワーカーの日常的なアドレスを持つ作業項目キューに試行されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

これは通常、まだ executive の作業項目を含むメモリを解放してドライバーで発生します。

 

 




