---
title: C28133
description: 警告 C28133 IoInitializeTimer は AddDevice から呼び出すことをお勧めします。
ms.assetid: c832cf67-1fc2-491b-a9e3-d35c5d9f6b73
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28133
ms.openlocfilehash: 6b07ca8a0cb47481e0b5673938d8a292b604cbd5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839595"
---
# <a name="c28133"></a>C28133


警告 C28133: IoInitializeTimer は AddDevice から呼び出すことをお勧めします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>IoInitializeTimer は、デバイスオブジェクトごとに1回だけ呼び出すことができます。 AddDevice ルーチンからこのメソッドを呼び出すと、予期せずに複数回呼び出されないようにすることができます。</p></td>
</tr>
</tbody>
</table>

 

ドライバーは、 **AddDevice**ルーチン以外のルーチンで[**ioinitializetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializetimer)を呼び出しています。 コード分析ツールは、この機会を使用して、エラーを回避し、ドライバーコードの信頼性を高めるためのベストプラクティスの推奨事項を提案します。

 

 





