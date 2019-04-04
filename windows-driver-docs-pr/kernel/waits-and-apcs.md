---
title: 待機および Apc
description: 待機および Apc
ms.assetid: b967beec-922c-4acf-a578-c476ce024fdb
keywords:
- カーネルのディスパッチャー オブジェクト WDK、アラート
- アラートのディスパッチャー オブジェクト WDK カーネル
- Apc WDK カーネル
- アラートの WDK カーネル
- カーネル ディスパッチャー オブジェクト WDK、Apc
- Apc のディスパッチャー オブジェクト WDK カーネル
- アラートのパラメーター
- WaitMode パラメーター
- カーネルのディスパッチャー オブジェクトを待機している WDK
- ディスパッチャー オブジェクト WDK カーネルは、を待つ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5536a081e269ab3905e3f080030f4ae77d20d2a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560229"
---
# <a name="waits-and-apcs"></a>待機および Apc





その待機を中断させるユーザー APC またはスレッドの終了のいずれかのユーザー モードの呼び出し元に代わってディスパッチャー オブジェクトを待っているスレッドを準備する必要があります。 スレッドを呼び出すと[ **kewaitforsingleobject の 1**](https://msdn.microsoft.com/library/windows/hardware/ff553350)、 [ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)、 [ **KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)、または[ **KeDelayExecutionThread**](https://msdn.microsoft.com/library/windows/hardware/ff551986)、オペレーティング システムが待機状態でスレッドを配置できます。 通常、オペレーティング システムには、呼び出し元を要求する操作が完了するまで、スレッドは待機状態に残ります。 ただし、呼び出し元が指定されている場合*WaitMode* = ユーザー モードでは、オペレーティング システムは、待機を中断可能性があります。 状態の NTSTATUS 値を持つルーチンが終了する場合、\_ユーザー\_APC します。

ドライバーで上記の 4 つのルーチンの 1 つを呼び出す*WaitMode* = UserMode 状態の戻り値を受け取る準備をする必要があります\_ユーザー\_APC します。 ドライバーは、状態とその現在の操作を完了する必要があります\_ユーザー\_APC をユーザー モードに制御を戻します。

オペレーティング システムが待機を中断する正確な状況は、の値によって異なります、 *Alertable*ルーチンのパラメーター。 場合*Alertable* = **TRUE**、待機が待機警告。 それ以外の場合、待機、警告不可能待機しています。 オペレーティング システムでは、ユーザーの APC を提供する場合のみアラート可能な待機を中断します。 オペレーティング システムでは、両方の種類のスレッドを終了するまで待機を中断します。

次の表では、さまざまなパラメーターの設定、待機、およびユーザー APC 配信間の関係について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>中断された待機しますか。</th>
<th>ユーザー APC が提供されるでしょうか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>警告</em> = <strong>TRUE</strong>
<em>WaitMode</em> = <strong>UserMode</strong></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><em>Alertable</em> = <strong>TRUE</strong>
<em>WaitMode</em> = <strong>KernelMode</strong></td>
<td><p>〇</p></td>
<td><p>X</p></td>
</tr>
<tr class="odd">
<td><em>警告</em> = <strong>FALSE</strong>
<em>WaitMode</em> = <strong>UserMode</strong></td>
<td><p>はい、スレッドの終了。 ユーザー テスト アプリケーションのいいえ</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><em>Alertable</em> = <strong>FALSE</strong>
<em>WaitMode</em> = <strong>KernelMode</strong></td>
<td><p>X</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>

 

スレッドのカーネルの Apc を無効にすることができます。 スレッド カーネル Apc を無効にするには、ユーザー APC 配信とそのスレッドのスレッドの終了の両方も無効となります。 Apc を無効にする方法の詳細については、[Apc を無効にすると](disabling-apcs.md)を参照してください。

アラート、使用頻度の低いのメカニズムは、オペレーティング システムの内部では、アラートの待機状態は中断もできます。 アラートは、待機を中断できる場合に*Alertable* = **TRUE**の値に関係なく、 *WaitMode*パラメーター。 待機中のルーチンは、状態の値を返します\_ALERTED します。

カーネル Apc が事前に、実行し、発生しないことを確認**KeWaitFor * Xxx*** または**KeDelayExecutionThread**を返します。 システムが中断し、内部的には、待機を再開します。 ドライバーは通常、このプロセスによって影響を受けませんが、ドライバーへの呼び出しなどの一時的な状態のディスパッチャー オブジェクト信号を見逃す可能性があります[ **KePulseEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552979)します。

 

 




