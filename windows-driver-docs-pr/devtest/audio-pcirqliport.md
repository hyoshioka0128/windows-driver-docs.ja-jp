---
title: PcIrqlIport ルール (オーディオ)
description: PcIrqlIport 規則は、PortCls ミニポートドライバーが正しい IRQL レベルで PortCls IPort インターフェイスを呼び出す必要があることを指定します。
ms.assetid: 59E22F37-3377-4B98-8613-EF5ED0CB63D9
ms.date: 05/21/2018
keywords:
- PcIrqlIport ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcIrqlIport
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e2b4e7a16c16ee29a2e3b4429e02b4706e49878
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917714"
---
# <a name="pcirqliport-rule-audio"></a>PcIrqlIport ルール (オーディオ)


PcIrqlIport 規則は、PortCls ミニポートドライバーが正しい IRQL レベルで PortCls IPort インターフェイスを呼び出す必要があることを指定します。

**ドライバーモデル: オーディオ**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071003) |

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

 

 

 





