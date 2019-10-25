---
title: C28114
description: 警告 C28114 IRP スタックエントリ全体をコピーすると、クリアまたは更新する必要がある特定のフィールドが初期化されたままになります。
ms.assetid: 39e3e313-e40f-4cb9-a534-c9e74fd1e88b
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28114
ms.openlocfilehash: 924409277079cecf27d8451a2ebbcf23b3f08b61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839601"
---
# <a name="c28114"></a>C28114


警告: C28114: IRP スタックエントリ全体をコピーすると、クリアまたは更新する必要がある特定のフィールドが初期化されたままになります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>これを実現するには、 <strong>Iocopyを</strong>使用します。</p></td>
</tr>
</tbody>
</table>

 

ドライバーが IRP を不適切にコピーしています。 IRP を不適切にコピーすると、データの損失やシステムのクラッシュなど、ドライバーに重大な問題が発生する可能性があります。 IRP をコピーする必要があり、 [**Iocopyに**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)よって実行される場合は、irp の特定のメンバーをコピーしたり、コピー後にゼロにする必要があります。

 

 





