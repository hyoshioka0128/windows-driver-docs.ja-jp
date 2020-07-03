---
title: PcAllocatedPages ルール (オーディオ)
description: PcAllocatedPages 規則は、PortCls ミニポートドライバーが、Allocatepg Formdl または AllocateContiguousPagesForMdl メソッドを呼び出すことによって、以前に割り当てられたページを解放することを指定します。
ms.assetid: C27B8D30-AE94-4B17-A45B-EBECB8A7B132
ms.date: 05/21/2018
keywords:
- PcAllocatedPages ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcAllocatedPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ab8421c5bbfa35d2f1687a9aca3cd16df6eaa02a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918128"
---
# <a name="pcallocatedpages-rule-audio"></a>PcAllocatedPages ルール (オーディオ)


PcAllocatedPages 規則は、PortCls ミニポートドライバーが、Allocatepg Formdl または AllocateContiguousPagesForMdl メソッドを呼び出すことによって、以前に割り当てられたページを解放することを指定します。

**ドライバーモデル: オーディオ**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071005) |

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
<td align="left"><p>この規則を確認するには、コマンドプロンプトウィンドウを開きます。 Driver Verifier コマンドを入力し、 <strong>/domain audio</strong>を指定します。</p>
<p>たとえば、次のように入力します。</p>
<p><strong>verifier/domain audio</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





