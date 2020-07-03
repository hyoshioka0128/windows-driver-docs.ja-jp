---
title: PcAllocateAndMapPages ルール (オーディオ)
description: PcAllocateAndMapPages 規則は、PortCls ミニポートドライバーが、正しいパラメーター IPortWaveRTStream AllocateAllocateContiguousPagesForMdl Formdliportwavertstream MapAllocatedPages を使用して、次のインターフェイスを呼び出すことを指定します。
ms.assetid: 32A3AA22-F387-460F-806E-82C5A0D52B73
ms.date: 05/21/2018
keywords:
- PcAllocateAndMapPages ルール (オーディオ)
topic_type:
- apiref
api_name:
- PcAllocateAndMapPages
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a44ec6cb7dbe7d50f7b4619490dbbafd38d39527
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918130"
---
# <a name="pcallocateandmappages-rule-audio"></a>PcAllocateAndMapPages ルール (オーディオ)


PcAllocateAndMapPages 規則は、正しいパラメーターを使用して、PortCls ミニポートドライバーが次のインターフェイスを呼び出すことを指定します。

-   IPortWaveRTStream:: AllocatePagesForMdl
-   IPortWaveRTStream:: AllocateContiguousPagesForMdl
-   IPortWaveRTStream:: MapAllocatedPages

**ドライバーモデル: オーディオ**

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー \_検証ツール \_ 検出 \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071009) |

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

 

 

 





