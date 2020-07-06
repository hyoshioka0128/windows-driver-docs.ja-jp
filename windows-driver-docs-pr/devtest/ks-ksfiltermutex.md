---
title: KsFilterMutex ルール ()
description: KsFilterMutex ルールは、KS ミニポートドライバーがフィルターミューテックスを取得し、正しい順序で解放することを指定します。
ms.assetid: 09927C42-2F05-49F6-AFE1-E45049ED2805
ms.date: 05/21/2018
keywords:
- KsFilterMutex ルール ()
topic_type:
- apiref
api_name:
- KsFilterMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d7dc2bb65b2096f128516136c89bff01f484820d
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968099"
---
# <a name="ksfiltermutex-rule-"></a>KsFilterMutex ルール ()


KsFilterMutex ルールは、KS ミニポートドライバーがフィルターミューテックスを取得し、正しい順序で解放することを指定します。

-   KS ミニポートドライバーは、フィルターミューテックスを再帰的に取得できません。
-   スレッドでは、最初に取得せずにフィルターミューテックスを解放しないでください。

**ドライバーモデル: KS**

**このルールでバグチェックが見つかりました**:[**バグチェック 0XC4: ドライバー \_ 検証ツールで \_ 検出された \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0008100A)


<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 ドライバー検証ツールコマンドを入力し、「 <strong>/domain ks</strong>」と指定します。</p>
<p>次に例を示します。</p>
<p></p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

**検証ツール (/domain** \[ )*オプション* \]**/driver** * &lt; ドライバー &gt; *を参照する
--------

[AVStream のフィルター制御ミューテックス](https://docs.microsoft.com/windows-hardware/drivers/stream/filter-control-mutex-in-avstream)
 

 





