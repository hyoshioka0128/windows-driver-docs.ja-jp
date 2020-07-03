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
ms.openlocfilehash: 88add45091a4f03a9b733b4a5328e29266addeba
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916368"
---
# <a name="pcunmapallocatedpages-rule-audio"></a>PcUnmapAllocatedPages ルール (オーディオ)


PcUnmapAllocatedPages ルールでは、次のことを指定します。

-   PortCls ミニポートドライバーは、最初にマップを解除せずに現在マップされている MDL をマップしません。
-   PortCls ミニポートドライバーは、 [IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)インターフェイスを使用して解放する前に、メモリを解除します。

**ドライバーモデル: オーディオ**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071004) |

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

 

 

 





