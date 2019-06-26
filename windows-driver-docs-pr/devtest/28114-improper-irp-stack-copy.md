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
ms.openlocfilehash: 574512fe4459111f41f538afcaec0d45b8f523f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364146"
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

 

ドライバーは IRP を正しくコピーは。 IRP を正しくコピーと、データとシステムのクラッシュの損失を含む、ドライバーでの重大な問題が発生することができます。 IRP をコピーする必要がある場合と[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)十分ではない、IRP の特定のメンバーは、コピーしてはならないか、コピーした後はゼロに設定する必要があります。

 

 





