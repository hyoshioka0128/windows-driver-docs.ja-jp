---
title: バグ チェック 0xC1 SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
description: SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION のバグ チェックでは、0x000000C1 の値を持ちます。 これは、ドライバーが特別なプールの無効なセクションに記述したことを示します。
ms.assetid: 4d5a3d95-de39-4e15-aba8-33257a6f0677
keywords:
- バグ チェック 0xC1 SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
- SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SPECIAL_POOL_DETECTED_MEMORY_CORRUPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c1f5826a4990d9b5cd2bff8fe6d922eec041968
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238518"
---
# <a name="bug-check-0xc1-specialpooldetectedmemorycorruption"></a>バグ チェック 0xC1:特別な\_プール\_検出\_メモリ\_破損


特殊な\_プール\_検出\_メモリ\_破損バグ チェックが 0x000000C1 の値を持ちます。 これは、ドライバーが特別なプールの無効なセクションに記述したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="specialpooldetectedmemorycorruption-parameters"></a>特別な\_プール\_検出\_メモリ\_破損パラメーター


パラメーター 4 では、違反の種類を示します。

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
<td align="left"><p>ドライバーを解放しようとしました。 アドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>ドライバーが割り当てられていないプールを解放しようとするとします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバーを解放しようとしました。 アドレス</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>(実際には、呼び出し元に特定) の計算</p></td>
<td align="left"><p>0x21、</p>
<p>0x22</p></td>
<td align="left"><p>ドライバーは、不適切なアドレスを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ドライバーを解放しようとしました。 アドレス</p></td>
<td align="left"><p>ビットが破損しているアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0x23</p></td>
<td align="left"><p>ドライバーは、アドレスを解放しますが、同じページ内で近くにあるバイトが破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ドライバーを解放しようとしました。 アドレス</p></td>
<td align="left"><p>ビットが破損しているアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0x24</p></td>
<td align="left"><p>ドライバーは、アドレスを解放しますが、割り当ての終了後に発生しているバイト数が上書きされました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>バイト数</p></td>
<td align="left"><p>0x30</p></td>
<td align="left"><p>無効な IRQL でプールを割り当てようとしたドライバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>ドライバーを解放しようとしました。 アドレス</p></td>
<td align="left"><p>0x31</p></td>
<td align="left"><p>ドライバーは、無効な IRQL でプールを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ドライバーを解放しようとしました。 アドレス</p></td>
<td align="left"><p>アドレスの 1 つのビットが破損しています</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0x32</p></td>
<td align="left"><p>ドライバーは、アドレスを解放しますが、同じページ内で近くにあるバイトが単一ビット エラーがあります。</p></td>
</tr>
</tbody>
</table>

 

\_プール\_ntddk.h の種類のコードが列挙されます。 具体的には、0 は非ページ プールを示しページ プールをいずれかを示します。

<a name="cause"></a>原因
-----

ドライバーは、特別なプールの無効なセクションに書き込まれます。

<a name="resolution"></a>解決方法
----------

現在のスレッドのバック トレースを取得します。 このバック トレースには、通常、エラーの原因が表示されます。

特別なプールについては、Windows ドライバー キットの Driver Verifier のセクションを参照してください。

 

 




