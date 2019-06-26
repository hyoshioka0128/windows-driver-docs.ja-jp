---
title: PnpRemove ルール (wdm)
description: PnpRemove ルールでは、ドライバーが IRP を完了できないことを指定します\_MN\_突然\_削除、IRP\_MN\_キャンセル\_削除\_デバイス、IRP\_MN\_キャンセル\_停止\_デバイス、または IRP\_MN\_削除\_デバイスの要求の失敗にします。
ms.assetid: 2713F943-36A2-41B9-B9C0-86FC06B22443
ms.date: 05/21/2018
keywords:
- PnpRemove ルール (wdm)
topic_type:
- apiref
api_name:
- PnpRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 155872a2df6ddd59254239a5ead63afd4e85aff5
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393680"
---
# <a name="pnpremove-rule-wdm"></a>PnpRemove ルール (wdm)


**PnpRemove**ルールでは、ドライバーが IRP を完了できないことを指定します\_MN\_突然\_削除、IRP\_MN\_キャンセル\_削除\_デバイス、IRP\_MN\_キャンセル\_停止\_デバイス、または IRP\_MN\_削除\_デバイスの要求の失敗にします。

> [!NOTE]
> Windows 8.1 でテストすることができます、 **PnpRemove**ルールを[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。 ルールが現在の使用可能なない[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)します。

 

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00043006) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

 

 





