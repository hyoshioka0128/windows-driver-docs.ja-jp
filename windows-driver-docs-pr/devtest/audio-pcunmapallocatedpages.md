---
title: PcUnmapAllocatedPages ルール (オーディオ)
description: PcUnmapAllocatedPages 規則は、PortCls ミニポートドライバーが現在マップされている MDL を最初にマップ解除せずにマップしないことを指定します。PortCls ミニポートドライバーは、IMiniportWaveRTStream インターフェイスを使用して解放する前に、メモリを解除します。
ms.assetid: 0ADF523C-9480-4AD2-8B98-23C95571CB0B
ms.date: 05/21/2018
keywords:
- PcUnmapAllocatedPages ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcUnmapAllocatedPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b237d2e0ea3c34261a8a06fdddcbe1ec630adc8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839583"
---
# <a name="pcunmapallocatedpages-rule-audio"></a>PcUnmapAllocatedPages ルール (オーディオ)


PcUnmapAllocatedPages ルールでは、次のことを指定します。

-   PortCls ミニポートドライバーは、最初にマップを解除せずに現在マップされている MDL をマップしません。
-   PortCls ミニポートドライバーは、 [IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)インターフェイスを使用して解放する前に、メモリを解除します。

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出され\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)が発生しました (0x00071004) |

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

 

 

 





