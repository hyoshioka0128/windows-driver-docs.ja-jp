---
title: PnpRemove ルール (wdm)
description: PnpRemove 規則は、ドライバーが IRP の突然の \_ 削除 \_ \_ 、irp が完了した \_ \_ \_ \_ デバイスの削除、irp のキャンセルを停止するデバイス \_ \_ \_ \_ 、または irp が \_ 失敗したデバイスの要求を \_ 削除 \_ できないことを指定します。
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
ms.openlocfilehash: 77f3266ac3e416888225f3869114246c2e4cb020
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917678"
---
# <a name="pnpremove-rule-wdm"></a>PnpRemove ルール (wdm)


**PnpRemove**規則は、ドライバーが irp の突然の \_ 削除 \_ 、irp が完了した \_ \_ \_ \_ \_ デバイスの削除、irp のキャンセルを停止するデバイス \_ \_ \_ \_ 、または irp が \_ 失敗したデバイスの要求を \_ 削除 \_ できないことを指定します。

> [!NOTE]
> Windows 8.1 では、[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を使用して**PnpRemove**の規則をテストできます。 このルールは、現在、[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)では使用できません。

 

**ドライバーモデル: WDM**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツールの \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00043006) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

 

 





