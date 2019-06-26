---
title: PcAllocateAndMapPages ルール (オーディオ)
description: PcAllocateAndMapPages ルールでは、PortCls ミニポート ドライバーが IPortWaveRTStream AllocatePagesForMdlIPortWaveRTStream AllocateContiguousPagesForMdl IPortWaveRTStream 正しいパラメーターを使用して、次のインターフェイスを呼び出すことを指定しますMapAllocatedPages します。
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
ms.openlocfilehash: ef3d060fc128938050182c7a28c2a854a5daf939
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391740"
---
# <a name="pcallocateandmappages-rule-audio"></a>PcAllocateAndMapPages ルール (オーディオ)


PortCls ミニポート ドライバーが、正しいパラメーターを使用して、次のインターフェイスを呼び出す PcAllocateAndMapPages ルールを指定します。

-   IPortWaveRTStream::AllocatePagesForMdl
-   IPortWaveRTStream::AllocateContiguousPagesForMdl
-   IPortWaveRTStream::MapAllocatedPages

|              |       |
|--------------|-------|
| ドライバー モデル | オーディオ |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00071009) |

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
<td align="left"><p>このルールを確認するには、コマンド プロンプト ウィンドウを開きます。 Driver Verifier のコマンドを入力し、指定<strong>/domain オーディオ</strong>します。</p>
<p>以下に例を示します。</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、次を参照してください。 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





