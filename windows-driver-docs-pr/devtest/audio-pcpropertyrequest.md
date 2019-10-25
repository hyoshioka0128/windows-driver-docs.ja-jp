---
title: PcPropertyRequest ルール (オーディオ)
description: PcPropertyRequest ルールでは、PortCls ミニポートドライバーが PcCompletePendingPropertyRequest を呼び出すことができないことを指定します。この要求は、状態が [保留中] の\_になります。
ms.assetid: 7D06F924-512F-4D21-98CD-B9E60CC8A6AB
ms.date: 05/21/2018
keywords:
- PcPropertyRequest ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcPropertyRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 679a0685714bb8d5fd9e8ba7ea5a33ec46921260
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839588"
---
# <a name="pcpropertyrequest-rule-audio"></a>PcPropertyRequest ルール (オーディオ)


PcPropertyRequest ルールでは、PortCls ミニポートドライバーが[**Pccompletependingpropertyrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)を呼び出すことができないことを指定します。この要求は、*状態が [* 保留中] の\_になります。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071008) |

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

 

 

 





