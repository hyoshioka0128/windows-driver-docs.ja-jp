---
title: PcIrqlDDIs ルール (オーディオ)
description: PcIrqlDDIs 規則は、PortCls ミニポートドライバーが正しい IRQL レベルで PortCls DDIs を呼び出す必要があることを指定します。
ms.assetid: 7CBC8407-FE46-449F-B921-883BCDA0436B
ms.date: 05/21/2018
keywords:
- PcIrqlDDIs ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcIrqlDDIs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b275bd654b0c71de58e1e135d0eb16ef198d7cde
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968417"
---
# <a name="pcirqlddis-rule-audio"></a>PcIrqlDDIs ルール (オーディオ)


PcIrqlDDIs 規則は、PortCls ミニポートドライバーが正しい IRQL レベルで PortCls DDIs を呼び出す必要があることを指定します。

**ドライバーモデル: オーディオ**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツールの \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071001)


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
<p>次に例を示します。</p>
<p><strong>verifier/domain audio</strong> [<em>オプション</em>] <strong>/driver</strong> <em> &lt; ドライバー &gt; </em>の設定</p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





