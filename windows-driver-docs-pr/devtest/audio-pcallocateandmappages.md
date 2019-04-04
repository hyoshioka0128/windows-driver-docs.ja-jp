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
ms.openlocfilehash: e568892800a4298fb335ca76108a65f2980d1d17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552542"
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
| この規則で見つかったバグ チェック | [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00071009) |

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
<p>次に、例を示します。</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

 

 





