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
ms.openlocfilehash: 0c4d2951e9e3e3f5a71b7543aa49056b5e4f7a6b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968367"
---
# <a name="pnpremove-rule-wdm"></a>PnpRemove ルール (wdm)


**PnpRemove**規則は、ドライバーが irp の突然の \_ 削除 \_ 、irp が完了した \_ \_ \_ \_ \_ デバイスの削除、irp のキャンセルを停止するデバイス \_ \_ \_ \_ 、または irp が \_ 失敗したデバイスの要求を \_ 削除 \_ できないことを指定します。

> [!NOTE]
> Windows 8.1 では、[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)を使用して**PnpRemove**の規則をテストできます。 このルールは、現在、[静的ドライバー検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)では使用できません。

 

**ドライバーモデル: WDM**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツールで \_ 検出された \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00043006)


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

 

 

 





