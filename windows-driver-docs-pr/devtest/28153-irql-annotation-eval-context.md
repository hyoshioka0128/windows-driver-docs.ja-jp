---
title: C28153
description: 警告の C28153 注釈から IRQL の値をこのコンテキストで評価できませんでした。
ms.assetid: 384d0925-b23b-4ba7-b5fb-34bb7106ca3f
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28153
ms.openlocfilehash: d7ce1480a9e51784b791044a69f54e3a0a015b7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557529"
---
# <a name="c28153"></a>C28153


C28153 を警告します。注釈から IRQL の値をこのコンテキストで評価できませんでした。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>可能性の高い注釈エラーです。</p>
<p>次の計算: &lt; <em>val</em>&gt;</p></td>
</tr>
</tbody>
</table>

 

この警告は、注釈が正しく作成されていないために、コード分析ツールが関数の注釈を解釈できないことを示します。 その結果、コード分析ツールは、指定した IRQL の値を特定できません。

この警告は、コード分析ツールは、IRQL の式を評価できません IRQL を話してドライバー固有の注釈のいずれかで発生します。

 

 





