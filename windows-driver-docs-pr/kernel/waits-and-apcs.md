---
title: 待機と APC
description: 待機と APC
ms.assetid: b967beec-922c-4acf-a578-c476ce024fdb
keywords:
- カーネルディスパッチャーオブジェクト WDK、アラート
- ディスパッチャーオブジェクト WDK カーネル、アラート
- Apc WDK カーネル
- WDK カーネルにアラートを生成します。
- カーネルディスパッチャーオブジェクト WDK、Apc
- ディスパッチャーオブジェクト WDK カーネル、Apc
- 警告可能パラメーター
- WaitMode パラメーター
- カーネルディスパッチャーオブジェクト WDK、待機中
- ディスパッチャーオブジェクト WDK カーネル、待機中
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6103b4f319cee1d3d16d60832cb57fffd910a2b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838321"
---
# <a name="waits-and-apcs"></a>待機と APC





ユーザーが呼び出しを中断するには、ユーザーの APC またはスレッドの終了によって、ユーザーモード呼び出し元に代わってディスパッチャーオブジェクトを待機するスレッドを準備する必要があります。 スレッドが[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)、 [**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)、 [**kewaitformutexobject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)、または[**kedelayexecutionthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)を呼び出すと、オペレーティングシステムはスレッドを待機状態にすることができます。 通常、スレッドは、呼び出し元が要求する操作をオペレーティングシステムが完了できるまで、待機状態のままにします。 ただし、呼び出し元で*Waitmode* = モードが指定されている場合、オペレーティングシステムは待機を中断する可能性があります。 この場合、ルーチンは、ユーザー\_APC の状態\_ユーザーの NTSTATUS 値で終了します。

*Waitmode* = ユーザー設定を使用して上記の4つのルーチンのいずれかを呼び出すドライバーは、\_ユーザー\_APC の戻り値を受け取るように準備する必要があります。 ドライバーは、現在の操作を\_ユーザー\_APC の状態で完了し、ユーザーモードに制御を返す必要があります。

オペレーティングシステムが待機を中断する正確な状況は、ルーチンの*警告*可能なパラメーターの値によって異なります。 *警告*可能 = **TRUE**の場合、待機は警告可能な待機です。 それ以外の場合、待機は、警告不可能な待機です。 オペレーティングシステムは、ユーザー APC を配信するためだけに、警告可能な待機を中断します。 オペレーティングシステムは、スレッドを終了するために、両方の種類の待機を中断します。

次の表では、さまざまなパラメーター設定、待機、およびユーザー APC 配信の関係について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>中断しますか?</th>
<th>ユーザー APC が配信されたか?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>警告</em>可能 = <strong>TRUE</strong>
<em>waitmode</em> <strong> = のモード</strong></td>
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
</tr>
<tr class="even">
<td> = <strong>TRUE</strong>
<em>Waitmode</em> = <strong>kernelmode で</strong>を<em>警告</em>する</td>
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
</tr>
<tr class="odd">
<td><em>警告</em>可能 = <strong>偽</strong>
<em>waitmode</em> <strong> = のモード</strong></td>
<td><p>はい (スレッドを終了する場合)。 いいえ (ユーザー Apc の場合)。</p></td>
<td><p>必須ではない</p></td>
</tr>
<tr class="even">
<td><em> = </em> <strong>偽</strong>
<em>waitmode</em> = <strong>kernelmode で</strong></td>
<td><p>必須ではない</p></td>
<td><p>必須ではない</p></td>
</tr>
</tbody>
</table>

 

スレッドに対してカーネル Apc を無効にすることができます。 スレッドに対してカーネル Apc を無効にすると、そのスレッドのユーザー APC 配信とスレッド終了の両方も無効になります。 Apc を無効にする方法の詳細については、「 [apc の無効化](disabling-apcs.md)」を参照してください。

アラートは、オペレーティングシステム内部のまれなメカニズムであり、警告可能な待機状態を中断することもできます。 アラートは、 *Waitmode*パラメーターの値に関係なく、警告 = **TRUE**の場合は*待機に割り込む*ことができます。 待機中のルーチンは、警告\_状態の値を返します。

カーネル Apc は事前にを実行しますが、 **Kewaitfor * Xxx*** または**Kedelayexecutionthread**はを返しません。 システムは割り込みを中断し、内部で待機を再開します。 通常、ドライバーはこのプロセスの影響を受けませんが、 [**KePulseEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kepulseevent)の呼び出しなど、一時的な状態に対して、ドライバーがディスパッチャーオブジェクトのシグナルを見逃してしまう可能性があります。

 

 




