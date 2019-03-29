---
title: 自動同期の使用
description: 自動同期の使用
ms.assetid: be7d3c0e-c3cf-4104-ab81-5ecdcb9163c8
keywords:
- WDK KMDF の同期
- WDK KMDF の自動同期
- ロックの WDK KMDF
- デバイス レベルの同期 WDK KMDF
- キュー レベルの同期 WDK KMDF
- WDK KMDF を同期なし
- 同期スコープ WDK KMDF
- 実行レベルを WDK KMDF
- WdfExecutionLevelPassive
- WdfExecutionLevelDispatch
- WdfExecutionLevelInheritFromParent
- WdfSynchronizationScopeDevice
- WdfSynchronizationScopeQueue
- WdfSynchronizationScopeNone
- WdfSynchronizationScopeInheritFromParent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e74574b2b899ce051eb80aa22a6c62809f1b514e
ms.sourcegitcommit: d028d25310ce028a3935bebf564d8092716903d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2019
ms.locfileid: "57254295"
---
# <a name="using-automatic-synchronization"></a>自動同期の使用


ほぼすべての framework ベースのドライバーのコードは、イベントのコールバック関数に存在します。 フレームワークは自動的に、ほとんどのドライバーのコールバック関数を次のように同期します。

-   フレームワークは常に同期[全般的なデバイス オブジェクト](https://msdn.microsoft.com/library/windows/hardware/dn265631#device-callbacks)、[機能のデバイス オブジェクト (FDO)](https://msdn.microsoft.com/library/windows/hardware/dn265631#fdo-callbacks)、および[物理デバイス オブジェクト (PDO)](https://msdn.microsoft.com/library/windows/hardware/dn265631#pdo-callbacks)各イベントのコールバック関数その他のためが 1 つだけのコールバック関数 (を除く[ *EvtDeviceSurpriseRemoval*](https://msdn.microsoft.com/library/windows/hardware/ff540913)、 [ *EvtDeviceQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff540883)、および[ *EvtDeviceQueryStop*](https://msdn.microsoft.com/library/windows/hardware/ff540885)) デバイスごとに一度に呼び出すことができます。 これらのコールバック関数は、プラグ アンド プレイ (PnP) および電源管理イベントをサポートし、IRQL で呼び出されます = パッシブ\_レベル。

-   必要に応じて、これらのコールバック関数は、一度に 1 つを実行できるように、フレームワークは、ドライバーの I/O 要求を処理するコールバック関数の実行を同期できます。 具体的には、フレームワークがのコールバック関数を同期できる[キュー](https://msdn.microsoft.com/library/windows/hardware/dn265647)、[割り込み](https://msdn.microsoft.com/library/windows/hardware/dn265640)、[遅延プロシージャ呼び出し (DPC)](https://msdn.microsoft.com/library/windows/hardware/dn265635)、[タイマー](https://msdn.microsoft.com/library/windows/hardware/dn265670)、[作業項目](https://msdn.microsoft.com/library/windows/hardware/dn265673)、および[ファイル](https://msdn.microsoft.com/library/windows/hardware/dn265638)オブジェクトの要求オブジェクトのほか、 [ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)コールバック関数。 フレームワークがほとんどを呼び出す IRQL でこれらのコールバック関数のディスパッチを =\_IRQL で実行するキューおよびファイル オブジェクトのコールバック関数を強制できますが、レベル = パッシブ\_レベル。 (作業項目のコールバック関数が常にパッシブで実行\_レベルです)。

フレームワークは、一連の内部同期ロックを使用して、この自動同期を実装します。 フレームワークにより、2 つまたは複数のスレッドが同時に、同じコールバック関数を呼び出すことはできませんので、各スレッドがコールバック関数を呼び出す前に同期ロックを獲得できるまで待機する必要があります。 (必要に応じて、ドライバーも取得できます必要な場合にこれらの同期ロック。 詳細については、次を参照してください[フレームワークを使用してロック](using-framework-locks.md)。)。

ドライバーはオブジェクト固有のデータを格納する必要があります[オブジェクト コンテキスト領域](framework-object-context-space.md)します。 ドライバーは、フレームワークで定義されたインターフェイスだけを使用している場合のみオブジェクトへのハンドルを受け取るコールバック関数はこのデータにアクセスできます。 フレームワークは、ドライバーのコールバック関数への呼び出しを同期している場合、一度に 1 つだけのコールバック関数が呼び出され、オブジェクトのコンテキストの空間は一度に 1 つだけのコールバック関数にアクセスします。

ドライバーを実装しない限り、[パッシブ レベル割り込み処理](supporting-passive-level-interrupts.md)そのサービスの割り込みのコード、および割り込みデータにアクセスがデバイスの IRQL (DIRQL) でを実行する必要があるあり、追加の同期が必要です。 詳細については、次を参照してください。[の同期を中断コード](synchronizing-interrupt-code.md)します。

場合、ドライバーは、I/O 要求を処理するコールバック関数の自動同期を有効、フレームワークは、一度に 1 つずつ実行するようこれらのコールバック関数を同期します。 次の表には、フレームワークを同期するコールバック関数が一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オブジェクトの種類</th>
<th align="left">同期されたコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>キュー オブジェクト</p></td>
<td align="left"><p><a href="request-handlers.md" data-raw-source="[Request handlers](request-handlers.md)">要求ハンドラー</a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541771" data-raw-source="[&lt;em&gt;EvtIoQueueState&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541771)"> <em>EvtIoQueueState</em></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541779" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541779)"> <em>EvtIoResume</em></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff541788" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541788)"> <em>EvtIoStop</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ファイル オブジェクト</p></td>
<td align="left"><p>すべて<a href="https://msdn.microsoft.com/library/windows/hardware/dn265638" data-raw-source="[callback functions](https://msdn.microsoft.com/library/windows/hardware/dn265638)">コールバック関数</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>オブジェクトを要求します。</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541817" data-raw-source="[&lt;em&gt;EvtRequestCancel&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541817)"><em>EvtRequestCancel</em></a></p></td>
</tr>
</tbody>
</table>

 

必要に応じて、フレームワークも同期できますこれら、割り込み、DPC、作業項目、コールバック関数と、デバイスのドライバーを提供するタイマー オブジェクトのコールバック関数 (割り込みオブジェクトの除外[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバック関数)。 この追加の同期を有効にするドライバーを設定する必要があります、 **AutomaticSerialization**これらのオブジェクトの構成構造体メンバー **TRUE**します。

要約すると、フレームワークの自動同期機能は、次の機能を提供します。

-   フレームワークは、各デバイスの PnP や電源管理のコールバック関数を常に同期します。

-   必要に応じて、フレームワークでは、I/O キューの要求のハンドラー、および (前の表を参照してください)、いくつかの追加のコールバック関数を同期できます。

-   ドライバーは、割り込み、DPC、用のコールバック関数を同期するためにフレームワークを問い合わせることができる作業項目、およびタイマー オブジェクト。

-   ドライバーは、割り込みサービスを提供するコードを同期する必要があり、アクセスが記載されている手法を使用してデータを中断[同期割り込みコード](synchronizing-interrupt-code.md)します。

-   フレームワークは同期しないドライバーのドライバーのなどの他のコールバック関数[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)コールバック関数、または I/O のターゲット オブジェクトを定義するコールバック関数。 代わりに、フレームワークによって追加[ロック](using-framework-locks.md)がこれらのコールバック関数を同期するドライバーを使用できます。

### <a name="choosing-a-synchronization-scope"></a>同期スコープを選択します。

フレームワークのすべてのデバイスの I/O キューのすべてに関連付けられているコールバック関数を同期させることができます。 また、framework が各デバイスの I/O キューのコールバック関数を個別に同期することができます。 ドライバーを使用できる同期オプションは次のとおりです。

-   デバイス レベルの同期

    フレームワークは、一度に 1 つずつ実行されるように、デバイスの I/O キューのすべての前の表に含まれているコールバック関数を同期します。 フレームワークは、コールバック関数を呼び出す前に、デバイスの同期ロックを取得することによって、この同期を実現します。

-   キュー レベルの同期

    フレームワークは、一度に 1 つずつ実行されるように各個々 の I/O キューの前の表に含まれているコールバック関数を同期します。 フレームワークは、コールバック関数を呼び出す前に、キューの同期ロックを取得することによって、この同期を実現します。

-   同期なし

    フレームワークは、前の表が含まれていて、コールバック関数を呼び出す前に同期ロックを取得しませんコールバック関数の実行を同期しません。 同期が必要な場合、ドライバーによって提供する必要があります。

デバイス レベルの同期、キュー レベルの同期、または、ドライバーのない同期を提供するためにフレームワークが必要かどうかを指定することを指定できます、*同期スコープ*ドライバー オブジェクトのデバイスオブジェクト、またはキューのオブジェクト。 **SynchronizationScope**のオブジェクトのメンバー [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造体がオブジェクトの識別します同期スコープ。 ドライバーが指定できる同期スコープの値は次のとおりです。

<a href="" id="wdfsynchronizationscopedevice"></a>**WdfSynchronizationScopeDevice**  
フレームワークは、デバイス オブジェクトの同期ロックを取得することで同期します。

<a href="" id="wdfsynchronizationscopequeue"></a>**WdfSynchronizationScopeQueue**  
フレームワークは、キュー オブジェクトの同期ロックを取得することで同期します。

<a href="" id="wdfsynchronizationscopenone"></a>**WdfSynchronizationScopeNone**  
フレームワークは同期しないと、同期ロックを取得できません。

<a href="" id="wdfsynchronizationscopeinheritfromparent"></a>**WdfSynchronizationScopeInheritFromParent**  
フレームワークの取得、オブジェクトの**SynchronizationScope**オブジェクトの親オブジェクトからの値。

一般に、デバイス レベルの同期を使用してはお勧めできません。

同期スコープの値の詳細については、次を参照してください。 [ **WDF\_同期\_スコープ**](https://msdn.microsoft.com/library/windows/hardware/ff552518)します。

ドライバー オブジェクトの既定の同期のスコープは**WdfSynchronizationScopeNone**します。 デバイスとキューのオブジェクトの既定の同期のスコープは**WdfSynchronizationScopeInheritFromParent**します。

すべてのデバイスのデバイス レベルの同期を行うために、フレームワークにする場合は、次の手順を使用できます。

1.  設定**SynchronizationScope**に**WdfSynchronizationScopeDevice**で、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)のドライバーの構造*ドライバー*オブジェクト。

2.  既定値を使用して、 **WdfSynchronizationScopeInheritFromParent**の各値*デバイス*オブジェクト。

または、個々 のデバイスのデバイス レベルの同期を提供するには、次の手順を使用することができます。

1.  既定値を使用して、 **WdfSynchronizationScopeNone**値、*ドライバー*オブジェクト。

2.  設定**SynchronizationScope**に**WdfSynchronizationScopeDevice**で、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)個々 の構造*デバイス*オブジェクト。

デバイスのキュー レベルの同期を提供するためにフレームワークを設定する場合は、次の手法を使用できます。

-   フレームワーク バージョン 1.9 以降では、設定して個々 のキューのキュー レベルの同期を有効する必要があります**WdfSynchronizationScopeQueue**で、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)キュー オブジェクトの構造体。 これは、手法をお勧めします。

-   または、すべての framework バージョンでは、次の手順を使用できます。
    1.  設定**SynchronizationScope**に**WdfSynchronizationScopeQueue**で、 [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)の構造、*デバイス*オブジェクト。
    2.  既定値を使用して、 **WdfSynchronizationScopeInheritFromParent**デバイスごとに値*キュー*オブジェクト。

ドライバーの I/O 要求を処理するコールバック関数を同期するためにフレームワークしたくない場合は、既定値を使用して**SynchronizationScope**ドライバーのドライバー、デバイス、およびキューのオブジェクトの値。 この場合、フレームワークが、ドライバーの I/O 要求に関連するコールバック関数を自動的に同期しないと、IRQL でコールバック関数を呼び出すことができます&lt;= ディスパッチ\_レベル。

その設定に注意してください、 **SynchronizationScope**値は、前の表が含まれています、コールバック関数のみを同期します。 場合に、ドライバーの割り込み、DPC、作業項目を同期させることも、フレームワークにして、タイマー オブジェクトのコールバック関数、ドライバーを設定する必要があります、 **AutomaticSerialization** にこれらのオブジェクトの構成構造体のメンバー**TRUE**します。

ただし、設定**AutomaticSerialization**に**TRUE**同じ IRQL で実行すべて同期するコールバック関数の場合にのみです。 選択、*実行レベル*、IRQL レベルの互換性のない可能性がありますが、次の説明です。 このような場合は、ドライバーを使用する必要があります[framework ロック](using-framework-locks.md)設定ではなく**AutomaticSerialization**します。 割り込み、DPC、構成構造体の詳細については、作業項目と、タイマー オブジェクトおよび設定に適用される制限について**AutomaticSerialization**これらの構造体、を参照してください。[**WDF\_INTERRUPT\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff552347)、 [ **WDF\_DPC\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff551296)、 [ **WDF\_WORKITEM\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff553086)、および[ **WDF\_タイマー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552519).

設定した場合**AutomaticSerialization**に**TRUE**、キュー レベルの同期を選択する必要があります。

### <a name="choosing-an-execution-level"></a>実行レベルを選択します。

ドライバーは、framework オブジェクトの一部の種類を作成するときに指定できます、*実行レベル*オブジェクト。 実行レベルでは、IRQL の位置、フレームワークが呼び出しますオブジェクトのイベント、ドライバーの I/O 要求を処理するコールバック関数を指定します。

ドライバーは、実行レベルを提供している場合、指定したレベルはキューおよびファイルのオブジェクトのコールバック関数に影響します。 通常、ドライバーの自動同期を使用している場合、フレームワークこれらのコールバック関数 IRQL でディスパッチを =\_レベル。 実行レベルを指定すると、ドライバーは IRQL でこれらのコールバック関数を呼び出すために、フレームワークを強制できます = パッシブ\_レベル。 オブジェクトのコールバック関数を呼び出すどのキューおよびファイルの IRQL を設定するときに、フレームワークは、次の規則を使用します。

-   ドライバーは、キューの自動同期を使用し、ファイル オブジェクトのコールバック関数は IRQL で呼び出されます場合 = ディスパッチ\_レベル、ドライバーは、IRQL でそのコールバック関数を呼び出すために、フレームワークを要求しない限り = パッシブ\_レベル。

-   IRQL でドライバーのキューおよびファイル オブジェクトのコールバック関数を呼び出すことができる場合、ドライバーは、自動同期を使用していないと、実行レベルを指定しない、 &lt;= ディスパッチ\_レベル。

ドライバーは、ファイル オブジェクトのコールバック関数を提供する場合 IRQL でこれらのコールバック関数を呼び出すために、フレームワークをするほとんどの場合は注意 = パッシブ\_レベルのため、一部のファイル、ファイル名などのデータの指定はページング可能な。

実行レベルを指定するには、ドライバーがの値を指定する必要があります、 **ExecutionLevel**のオブジェクトのメンバー [ **WDF\_オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)構造体。 ドライバーを指定する実行レベルの値は次のとおりです。

<a href="" id="wdfexecutionlevelpassive"></a>**WdfExecutionLevelPassive**  
フレームワークでは、オブジェクトのコールバック関数を呼び出す IRQL でパッシブ =\_レベル。

<a href="" id="wdfexecutionleveldispatch"></a>**WdfExecutionLevelDispatch**  
フレームワークは、IRQL でオブジェクトのコールバック関数を呼び出すことができます&lt;= ディスパッチ\_レベル。 (ドライバーを使用しているフレームワークを常に自動的に同期コールバック関数の呼び出し IRQL = ディスパッチ\_レベルです)。

<a href="" id="wdfexecutionlevelinheritfromparent"></a>**WdfExecutionLevelInheritFromParent**  
フレームワークの取得、オブジェクトの**ExecutionLevel**オブジェクトの親からの値。

ドライバー オブジェクトの既定の実行レベルは**WdfExecutionLevelDispatch**します。 その他のすべてのオブジェクトの既定の実行レベルは**WdfExecutionLevelInheritFromParent**します。

実行レベル値の詳細については、次を参照してください。 [ **WDF\_実行\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff551310)します。

次の表では、位置、フレームワークは、キュー オブジェクトとファイル オブジェクトのドライバーのコールバック関数を呼び出すことができます、IRQL レベルを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">同期スコープ</th>
<th align="left">実行レベル</th>
<th align="left">IRQL のキューおよびファイルのコールバック関数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>WdfSynchronizationScopeDevice</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfSynchronizationScopeDevice</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelDispatch</strong></p></td>
<td align="left"><p>DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>WdfSynchronizationScopeQueue</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfSynchronizationScopeQueue</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelDispatch</strong></p></td>
<td align="left"><p>DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>WdfSynchronizationScopeNone</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>WdfSynchronizationScopeNone</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelDispatch</strong></p></td>
<td align="left"><p>&lt;= DISPATCH_LEVEL</p></td>
</tr>
</tbody>
</table>

 

レベルを実行を設定することができます**WdfExecutionLevelPassive**または**WdfExecutionLevelDispatch**ドライバー、デバイス、ファイル、キュー、タイマー、および一般的なオブジェクト。 他のオブジェクトのみの**WdfExecutionLevelInheritFromParent**は許可されています。

指定する必要があります**WdfExecutionLevelPassive**場合。

-   ドライバーのコールバック関数は、framework のメソッドまたは IRQL でのみ呼び出すことができる Windows Driver Model (WDM) ルーチンを呼び出す必要があります = パッシブ\_レベル。

-   ドライバーのコールバック関数は、ページング可能なコードやデータにアクセスする必要があります。 (たとえば、ファイル オブジェクトのコールバック関数通常アクセス ページング可能なデータ)。

設定ではなく**WdfExecutionLevelPassive**には、ドライバーを設定できます**WdfExecutionLevelDispatch**を作成するコールバック関数を提供および[作業項目](using-framework-work-items.md)場合する必要がありますIRQL でいくつかの操作を処理 = パッシブ\_レベル。

かどうかは、結果セット オブジェクトの実行レベルを決定する前に**WdfExecutionLevelPassive**には、ドライバーとドライバー スタックの他のドライバーを呼び出される位置の IRQL を決定する必要があります。 次の状況を考慮してください。

-   IRQL でドライバーをシステムが通常は呼び出します、ドライバーが、カーネル モード ドライバー スタックの上部にある場合、パッシブ =\_レベル。 このようなドライバーのクライアントには、UMDF ドライバーまたはユーザー モード アプリケーションがあります。 指定する**WdfExecutionLevelPassive**は悪影響を与えたり、ドライバーのパフォーマンスに影響を与える、フレームワークが作業項目の IRQL で呼び出されるドライバーの呼び出しをキューに登録があるないために = パッシブ\_レベル。

-   スタックの上部にある、ドライバーがない場合、システムは可能性がありますを呼び出しませんドライバー IRQL でパッシブ =\_レベル。 そのため、フレームワークのドライバーの呼び出しを作業項目に IRQL で後でと呼ばれる必要がありますキュー = パッシブ\_レベル。 このプロセスには、不適切なドライバーのパフォーマンス、IRQL で呼び出されるドライバーのコールバック関数を許可すると比較した可能性があります&lt;= ディスパッチ\_レベル。

DPC オブジェクト、およびタイマー オブジェクトを表していない[パッシブ レベル タイマー](using-timers.md)、設定することはできません注、 **AutomaticSerialization**構成構造体のメンバー**は TRUE。** レベルを親デバイスの実行を設定している場合**WdfExecutionLevelPassive**します。 これは、フレームワークが、デバイス オブジェクトの取得するため[コールバック同期ロック](using-framework-locks.md)IRQL = パッシブ\_DPC またはタイマー オブジェクトのコールバック関数の同期に、ロックは使用できませんレベルとIRQL で実行する必要があります = ディスパッチ\_レベル。 このような場合は、ドライバーを使用する必要があります[framework スピン ロック](using-framework-locks.md#framework-spin-locks)で任意のデバイス、DPC、またはタイマー オブジェクトのコールバック関数で相互に同期する必要があります。

タイマー オブジェクトを注も*は*パッシブ レベル タイマーを表すが、設定することができます、 **AutomaticSerialization**を TRUE に設定の構造体のメンバー*のみ*親デバイスの実行レベルに設定されている場合**WdfExecutionLevelPassive**します。

 

 





