---
title: KsProcessingMutex ルール ()
ms.assetid: AD73B241-7B08-4E48-94A1-B6BDE78590E6
ms.date: 05/21/2018
description: ''
keywords:
- KsProcessingMutex ルール ()
topic_type:
- apiref
api_name:
- KsProcessingMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b30f77019b29dfab72d5f14cf9e761db13248a2
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968147"
---
# <a name="ksprocessingmutex-rule-"></a>KsProcessingMutex ルール ()


KsProcessingMutex ルールは、KS ミニポートドライバーが処理ミューテックスを正しい順序で使用することを指定します。

-   処理ミューテックスを再帰的に取得することはできません。
-   処理ミューテックスを取得したスレッドは、その後フィルターコントロールのミューテックスを取得しようとすることはできません。
-   スレッドでは、最初に処理ミューテックスを取得せずに解放しないでください。

**ドライバーモデル: KS**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0008100b)


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
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>関連項目
--------

[AVStream でのミューテックスの処理](https://docs.microsoft.com/windows-hardware/drivers/stream/processing-mutex-in-avstream)
 

 





