---
title: StorPortSpinLock3 ルール (storport)
description: StorPortSpinLock3 ルールは、StorPortAcquireSpinLock ルーチンのドキュメントで説明されているロックの取得の階層を確認します。
ms.assetid: EC637CBD-A45D-44C6-8FAA-7035A36144B6
ms.date: 05/21/2018
keywords:
- StorPortSpinLock3 ルール (storport)
topic_type:
- apiref
api_name:
- StorPortSpinLock3
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9350e74b8a579f7847090ee378179775fc95a664
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391808"
---
# <a name="storportspinlock3-rule-storport"></a>StorPortSpinLock3 ルール (storport)


**StorPortSpinLock3**ルールの検証のドキュメントで説明されているロックの取得の階層、 [ **StorPortAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportacquirespinlock)ルーチン。

Storport ミニポート ドライバーでは、既に保持されているロックの取得を間違った順序でロックを取得したりしないことを確認してください。 これらの誤りのいずれかにより、システムのデッドロックが発生します。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>StorPortSpinLock3</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**StorPortAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportacquirespinlock)
 

 





