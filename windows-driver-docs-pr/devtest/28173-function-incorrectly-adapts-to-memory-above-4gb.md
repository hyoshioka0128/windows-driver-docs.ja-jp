---
title: C28173
description: 警告の C28173 が正しくない 4 GB を超える物理メモリに合わせて、現在の関数が表示されます。
ms.assetid: 9332c35e-9d04-4286-9eff-3a639589607e
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28173
ms.openlocfilehash: a25831462041752a09ea48d40ae9f1146d65f9dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371482"
---
# <a name="c28173"></a>C28173


C28173 を警告します。正しくない 4 GB を超える物理メモリに合わせて、現在の関数が表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>呼び出しからの回復には、コードが表示されない<strong>IoGetDmaAdapter</strong>マップ レジスタの数が少ないを返します。 詳細については、ドキュメントを参照してください。</p></td>
</tr>
</tbody>
</table>

 

4 GB を超えるメモリを搭載したシステムで、 **IoGetDmaAdapter**要求よりもレジスタにマップ少ない関数が返す可能性があります。 これは、要求された値が大きい (64 近づいている) 可能性が高いとなります。これは、4 GB より下の領域に 4 GB を超える物理メモリをマップする必要があるのためです。

よく寄せられるよりも少ないレジスタを取得するコードが適応しない場合、この警告メッセージが表示されます。 関数への呼び出しは、いつ**IoGetDmaAdapter**、コード分析ツールをシミュレートする、 **IoGetDmaAdapter**要求よりも小さい番号のレジスタを返します。 呼び出し元の関数は、この条件を処理し、正常に完了する必要があります。

ドライバーが 4 GB 以上のシステムで失敗できるその他の方法があることに注意してください。 これらの考えられる障害モードのコードを調査する必要があります。 詳細については、4 GB のメモリの問題と、マップのレジスタは、次を参照してください。 [ **NdisMAllocateMapRegisters**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff552300(v=vs.85))します。

 

 





