---
title: PcRegisterAdapterPower rule (オーディオ)
description: PcregiPortCls Adapter電源ルールでは、PcUnregisterAdapterPowerManagement の呼び出しを介在させずに、Pcregi Adapterpowermanagement を2回呼び出すことができないことを指定します。最初に PcRegisterAdapterPowerManagement を呼び出しています。
ms.assetid: 8F6E6B1D-F19C-469A-BC5A-061996BEA532
ms.date: 05/21/2018
keywords:
- PcRegisterAdapterPower rule (オーディオ)
topic_type:
- apiref
api_name:
- PcRegisterAdapterPower
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 658cf524fd606f5c5d81109b39c7f8559b4db683
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839586"
---
# <a name="pcregisteradapterpower-rule-audio"></a>PcRegisterAdapterPower rule (オーディオ)


PcregiPortCls Adapterpower rule は、次のようにして、ミニミニポートドライバーが以下を実行しないように指定します。

-   [**Pcunregisteradapterpowermanagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)の呼び出しを介在させずに、 [**pcregisteradapterpowermanagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)を2回呼び出します。
-   最初に[**Pcregisteradapterpowermanagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)を呼び出さずに[**pcunregisteradapterpowermanagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)を呼び出します。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071006) |

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

 

 

 





