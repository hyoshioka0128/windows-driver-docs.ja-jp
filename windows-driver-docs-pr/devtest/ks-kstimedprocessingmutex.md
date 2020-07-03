---
title: KsTimedProcessingMutex rule ()
description: KsTimedProcessingMutex ルールは、KS ミニポートドライバーが100ミリ秒を超える処理ミューテックスを保持しないことを指定します。
ms.assetid: 18246AAE-6328-4171-973E-4C762CF719AE
ms.date: 05/21/2018
keywords:
- KsTimedProcessingMutex rule ()
topic_type:
- apiref
api_name:
- KsTimedProcessingMutex
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6ff3417336142578e9f11dee0167a72a5274f82f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917962"
---
# <a name="kstimedprocessingmutex-rule-"></a>KsTimedProcessingMutex rule ()


KsTimedProcessingMutex ルールは、KS ミニポートドライバーが100ミリ秒を超える処理ミューテックスを保持しないことを指定します。

**ドライバーモデル: KS**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00082005) |

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
<p>たとえば、次のように入力します。</p>
<p><strong>verifier/domain ks</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

<a name="see-also"></a>こちらもご覧ください
--------

[AVStream でのミューテックスの処理](https://docs.microsoft.com/windows-hardware/drivers/stream/processing-mutex-in-avstream)
 

 





