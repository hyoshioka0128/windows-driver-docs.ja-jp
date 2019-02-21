---
title: C28133
description: 警告 C28133 IoInitializeTimer は AddDevice から最も呼び出されます。
ms.assetid: c832cf67-1fc2-491b-a9e3-d35c5d9f6b73
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28133
ms.openlocfilehash: 0ed3998850b8ea85fa62039ae5d5cdc07695c68c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550872"
---
# <a name="c28133"></a>C28133


C28133 を警告します。IoInitializeTimer は AddDevice から最もと呼ばれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>IoInitializeTimer は、デバイス オブジェクトあたり 1 回のみ呼び出すことができます。 ルーチン、AddDevice から呼び出すことが呼び出されない点が予期せず複数回の保証役立ちます。</p></td>
</tr>
</tbody>
</table>

 

ドライバーを呼び出す[ **IoInitializeTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff549344)以外のルーチンでその**AddDevice**ルーチン。 コード分析ツールは、エラーを防止し、ドライバー コードの信頼性を高めることができますベスト プラクティス推奨事項を提案する、この機会を使用しています。

 

 





