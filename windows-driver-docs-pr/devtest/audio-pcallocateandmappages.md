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
ms.openlocfilehash: 48debd629dea2352a4f083d48c789d9df34b2fda
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968423"
---
# <a name="pcallocateandmappages-rule-audio"></a>PcAllocateAndMapPages ルール (オーディオ)


PcAllocateAndMapPages 規則は、正しいパラメーターを使用して、PortCls ミニポートドライバーが次のインターフェイスを呼び出すことを指定します。

-   IPortWaveRTStream:: AllocatePagesForMdl
-   IPortWaveRTStream:: AllocateContiguousPagesForMdl
-   IPortWaveRTStream:: MapAllocatedPages

**ドライバーモデル: オーディオ**

**このルールでバグチェックが見つかりまし**た:[**バグチェック 0XC4: ドライバー \_ 検証ツールで \_ 検出された \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00071009)


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

 

 

 





