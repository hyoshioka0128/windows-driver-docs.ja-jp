---
title: PcPoRequestPowerIrp ルール (オーディオ)
description: このルールは、PortCls ミニポートドライバーが、\_の電源\_設定された IRP\_を持つ PoRequestPowerIrp を呼び出さないことを確認します。
ms.assetid: 9AF26E98-CB8A-41F1-BF40-1B5FBFD04550
ms.date: 05/21/2018
keywords:
- PcPoRequestPowerIrp ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcPoRequestPowerIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d677e729fd9ab7facf1a9e055b4ec5f47a4ee23f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839337"
---
# <a name="pcporequestpowerirp-rule-audio"></a>PcPoRequestPowerIrp ルール (オーディオ)


このルールは、PortCls ミニポートドライバーが、 [ **\_の電源\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された IRP\_を持つ[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出さないことを確認します。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0007100A) |

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
<p>次に、例を示します。</p>
<p><strong>verifier/domain audio</strong> [<em>オプション</em>] <strong>/driver</strong> <em>&lt;ドライバー&gt;</em></p>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





