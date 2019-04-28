---
title: C28114
description: 全体の IRP 警告 C28114 コピー フィールドを初期化する特定のスタック エントリ リーフはクリアまたは更新します。
ms.assetid: 39e3e313-e40f-4cb9-a534-c9e74fd1e88b
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28114
ms.openlocfilehash: 7bab641cbf7f420e73c2e1574bd8bef686f25ec5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361436"
---
# <a name="c28114"></a>C28114


警告:C28114:初期化をクリアまたは更新する必要がある特定のフィールドのまま、IRP スタック エントリ全体をコピーします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>使用<strong>IoCopyCurrentIrpStackLocationToNext</strong>これを実現するには</p></td>
</tr>
</tbody>
</table>

 

ドライバーは IRP を正しくコピーは。 IRP を正しくコピーと、データとシステムのクラッシュの損失を含む、ドライバーでの重大な問題が発生することができます。 IRP をコピーする必要がある場合と[ **IoCopyCurrentIrpStackLocationToNext** ](https://msdn.microsoft.com/library/windows/hardware/ff548387)十分ではない、IRP の特定のメンバーは、コピーしてはならないか、コピーした後はゼロに設定する必要があります。

 

 





