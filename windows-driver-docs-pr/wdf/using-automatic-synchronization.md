---
title: 自動同期の使用
description: 自動同期の使用
ms.assetid: be7d3c0e-c3cf-4104-ab81-5ecdcb9163c8
keywords:
- WDK KMDF の同期
- 自動同期 WDK KMDF
- WDK KMDF のロック
- デバイスレベルの同期 WDK KMDF
- キューレベルの同期 WDK KMDF
- 同期 WDK KMDF なし
- 同期スコープ WDK KMDF
- 実行レベル WDK KMDF
- WdfExecutionLevelPassive
- WdfExecutionLevelDispatch
- WdfExecutionLevelInheritFromParent
- Wdf同期スコープデバイス
- Wdf同期 Scopequeue
- WdfSynchronizationScopeNone
- Wdf同期 Scopeinheritfromparent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd779bf73e8b8f8ea5d8a65dcd15f1910cf5224d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843092"
---
# <a name="using-automatic-synchronization"></a>自動同期の使用


フレームワークベースのドライバーのほとんどすべてのコードは、イベントコールバック関数に存在します。 次のように、フレームワークによって、ドライバーのほとんどのコールバック関数が自動的に同期されます。

-   フレームワークは、[一般的なデバイスオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#device-callbacks)、[機能デバイスオブジェクト (FDO)](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#fdo-callbacks)、および[物理デバイスオブジェクト (PDO)](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#pdo-callbacks)イベントコールバック関数を互いに同期します。これにより、各デバイスに対して1つのコールバック関数 ( [*EvtDeviceSurpriseRemoval*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_surprise_removal)、 [*Evtdevicequeryremove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_remove)、および[*evtdevicequeryremove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_query_stop)) を一度に呼び出すことができます。 これらのコールバック関数は、プラグアンドプレイ (PnP) および電源管理イベントをサポートし、IRQL = パッシブ\_レベルで呼び出されます。

-   必要に応じて、フレームワークは、ドライバーの i/o 要求を処理するコールバック関数の実行を同期して、これらのコールバック関数が一度に1つずつ実行されるようにすることができます。 具体的には、フレームワークは、[キュー](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/)、[割り込み](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/)、[遅延プロシージャ呼び出し (DPC)](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/)、[タイマー](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/)、[作業項目](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/)、および[ファイル](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/)オブジェクトのコールバック関数を、要求オブジェクトの[*EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数。 このフレームワークは、IRQL = ディスパッチ\_レベルでこれらのコールバック関数のほとんどを呼び出しますが、キューおよびファイルオブジェクトのコールバック関数を IRQL = パッシブ\_レベルで実行するように強制することができます。 (作業項目のコールバック関数は、常にパッシブ\_レベルで実行します)。

フレームワークは、一連の内部同期ロックを使用して、この自動同期を実装します。 このフレームワークにより、2つ以上のスレッドが同時に同じコールバック関数を呼び出すことができなくなります。これは、各スレッドが、コールバック関数を呼び出す前に同期ロックを取得できるようになるまで待機する必要があるためです。 (オプションで、ドライバーは必要に応じてこれらの同期ロックを取得することもできます。 詳細については、「 [Using Framework Locks](using-framework-locks.md)」を参照してください)。

ドライバーは、オブジェクトの[コンテキスト空間](framework-object-context-space.md)にオブジェクト固有のデータを格納する必要があります。 ドライバーがフレームワークによって定義されたインターフェイスのみを使用する場合、オブジェクトへのハンドルを受け取るコールバック関数だけがこのデータにアクセスできます。 フレームワークがドライバーのコールバック関数の呼び出しを同期している場合、一度に呼び出されるコールバック関数は1つだけで、オブジェクトのコンテキスト空間は一度に1つのコールバック関数にしかアクセスできません。

ドライバーが[パッシブレベルの割り込み処理](supporting-passive-level-interrupts.md)を実装していない限り、サービスの割り込みと割り込みデータへのアクセスを行うコードは、デバイスの IRQL (dirql) で実行する必要があり、追加の同期が必要です。 詳細については、「[割り込みコードの同期](synchronizing-interrupt-code.md)」を参照してください。

ドライバーで i/o 要求を処理するコールバック関数の自動同期が有効になっている場合、フレームワークはこれらのコールバック関数を同期して、一度に1つずつ実行されるようにします。 次の表に、フレームワークによって同期されるコールバック関数を示します。

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
<td align="left"><p>Queue オブジェクト</p></td>
<td align="left"><p><a href="request-handlers.md" data-raw-source="[Request handlers](request-handlers.md)">要求ハンドラー</a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state" data-raw-source="[&lt;em&gt;EvtIoQueueState&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_state)"><em>evtioqueuestate</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume" data-raw-source="[&lt;em&gt;EvtIoResume&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)"><em>EvtIoResume</em></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop" data-raw-source="[&lt;em&gt;EvtIoStop&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)"><em>evtiostop</em></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ファイルオブジェクト</p></td>
<td align="left"><p>すべての<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/" data-raw-source="[callback functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/)">コールバック関数</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>要求オブジェクト</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel" data-raw-source="[&lt;em&gt;EvtRequestCancel&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)"><em>EvtRequestCancel</em></a></p></td>
</tr>
</tbody>
</table>

 

また、必要に応じて、これらのコールバック関数を、ドライバーがデバイスに提供する割り込み、DPC、作業項目、およびタイマーオブジェクトのコールバック関数と同期させることもできます (interrupt オブジェクトの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバックは除く)。関数)。 この追加の同期を有効にするには、ドライバーは、これらのオブジェクトの構成構造体の自動**シリアル化**メンバーを**TRUE**に設定する必要があります。

概要として、フレームワークの自動同期機能には、次の機能が用意されています。

-   フレームワークは、各デバイスの PnP と電源管理のコールバック関数を常に同期します。

-   必要に応じて、フレームワークは、i/o キューの要求ハンドラーと、いくつかの追加のコールバック関数を同期できます (前の表を参照)。

-   ドライバーは、割り込み、DPC、作業項目、およびタイマーオブジェクトのコールバック関数を同期するようにフレームワークに要求できます。

-   ドライバーは、割り込み[コードの同期](synchronizing-interrupt-code.md)に関するページで説明されている手法を使用して、サービスが中断し、割り込みデータにアクセスするコードを同期する必要があります。

-   このフレームワークでは、ドライバーのその他のコールバック関数 (ドライバーの[*補完ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine)のコールバック関数など) や、i/o ターゲットオブジェクトで定義されているコールバック関数とは同期しません。 代わりに、このフレームワークには、ドライバーがこれらのコールバック関数を同期するために使用できる追加の[ロック](using-framework-locks.md)が用意されています。

### <a name="choosing-a-synchronization-scope"></a>同期スコープの選択

すべてのデバイスの i/o キューに関連付けられているすべてのコールバック関数を、フレームワークで同期するように選択できます。 または、各デバイスの i/o キューのコールバック関数をフレームワークで個別に同期するように選択することもできます。 ドライバーで使用できる同期オプションは次のとおりです。

-   デバイスレベルの同期

    フレームワークは、デバイスのすべての i/o キューについて、前のテーブルに格納されているコールバック関数を同期して、一度に1つずつ実行します。 フレームワークは、コールバック関数を呼び出す前にデバイスの同期ロックを取得することによって、この同期を実現します。

-   キューレベルの同期

    フレームワークは、個々の i/o キューごとに、前のテーブルに格納されているコールバック関数を同期して、一度に1つずつ実行します。 フレームワークは、コールバック関数を呼び出す前に、キューの同期ロックを取得することによって、この同期を実現します。

-   同期なし

    フレームワークは、前のテーブルに含まれているコールバック関数の実行を同期しません。また、コールバック関数を呼び出す前に、同期ロックを取得しません。 同期が必要な場合は、ドライバーによって提供される必要があります。

フレームワークでデバイスレベルの同期、キューレベルの同期、またはドライバーの同期を提供するかどうかを指定するには、ドライバーオブジェクト、デバイスオブジェクト、またはキューオブジェクトの*同期スコープ*を指定します。 オブジェクトの[**WDF\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)の同期スコープメンバー\_属性構造は、オブジェクトの同期スコープを**識別します**。 ドライバーが指定できる同期スコープの値は次のとおりです。

<a href="" id="wdfsynchronizationscopedevice"></a>**Wdf同期スコープデバイス**  
フレームワークは、デバイスオブジェクトの同期ロックを取得することによって同期します。

<a href="" id="wdfsynchronizationscopequeue"></a>**Wdf同期 Scopequeue**  
フレームワークは、キューオブジェクトの同期ロックを取得することによって同期します。

<a href="" id="wdfsynchronizationscopenone"></a>**WdfSynchronizationScopeNone**  
このフレームワークは同期されず、同期ロックも取得されません。

<a href="" id="wdfsynchronizationscopeinheritfromparent"></a>**Wdf同期 Scopeinheritfromparent**  
フレームワークは、オブジェクトの親オブジェクトからオブジェクトの**同期スコープ**値を取得します。

一般に、デバイスレベルの同期は使用しないことをお勧めします。

同期スコープの値の詳細については、「 [**WDF\_synchronization\_scope**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_synchronization_scope)」を参照してください。

ドライバーオブジェクトの既定の同期スコープは**WdfSynchronizationScopeNone**です。 デバイスとキューオブジェクトの既定の同期スコープは、 **Wdfsynchronization Scopeinheritfromparent**です。

フレームワークですべてのデバイスに対してデバイスレベルの同期を提供する場合は、次の手順を実行します。

1.  [**WDF\_オブジェクトの\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体に、**同期スコープ**を**wdf同期 scopedevice**に設定します。

2.  各*デバイス*オブジェクトに対して、既定の**Wdf同期 Scopeinheritfromparent**値を使用します。

また、個々のデバイスにデバイスレベルの同期を提供するには、次の手順を実行します。

1.  *Driver*オブジェクトの既定の**WdfSynchronizationScopeNone**値を使用します。

2.  個々の*デバイス*オブジェクトの[**属性構造\_、WDF\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)で、**同期スコープ**を**wdf scopedevice**に設定します。

フレームワークでデバイスのキューレベルの同期を提供する場合は、次の手法を使用できます。

-   Framework バージョン1.9 以降では、キューオブジェクトの[**属性構造\_WDF\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)で**Wdfsynchronization scopequeue**を設定して、個々のキューに対してキューレベルの同期を有効にする必要があります。 これは推奨される方法です。

-   または、すべてのフレームワークバージョンで次の手順を使用することもできます。
    1.  *デバイス*オブジェクトの[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造で、**同期スコープ**を**wdf scopequeue**に設定します。
    2.  各デバイスの*キュー*オブジェクトに対して、既定の**Wdf同期 scopefromparent**値を使用します。

ドライバーの i/o 要求を処理するコールバック関数をフレームワークが同期しないようにするには、ドライバーのドライバー、デバイス、およびキューオブジェクトの既定の**同期スコープ**値を使用します。 この場合、フレームワークはドライバーの i/o 要求に関連するコールバック関数を自動的には同期しません。また、コールバック関数は、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。

同期**スコープ**値を設定すると、前のテーブルに含まれているコールバック関数だけが同期されることに注意してください。 また、ドライバーの割り込み、DPC、作業項目、およびタイマーオブジェクトのコールバック関数をフレームワークに同期させる場合は、ドライバーがこれらのオブジェクトの構成構造体の自動**シリアル化**メンバーを**TRUE**に設定する必要があります。

ただし、同期するすべてのコールバック関数が同じ IRQL で実行される場合にのみ、自動**シリアル化**を**TRUE**に設定できます。 次に説明する*実行レベル*を選択すると、互換性のない IRQL レベルが生じる可能性があります。 このような状況では、ドライバーは自動**シリアル化**を設定する代わりに、[フレームワークロック](using-framework-locks.md)を使用する必要があります。 割り込み、DPC、作業項目、タイマーオブジェクトの構成構造、およびこれらの構造での自動**シリアル化**の設定に適用される制限の詳細については、「 [**WDF\_interrupt」を参照してください。\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)、 [**WDF\_DPC\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/ns-wdfdpc-_wdf_dpc_config)、 [**WDF\_WORKITEM\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/ns-wdfworkitem-_wdf_workitem_config)、および[**WDF\_TIMER\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)。

自動**シリアル化**を**TRUE**に設定した場合は、[キューレベルの同期] を選択する必要があります。

### <a name="choosing-an-execution-level"></a>実行レベルの選択

ドライバーは、何らかの種類のフレームワークオブジェクトを作成するときに、そのオブジェクトの*実行レベル*を指定できます。 実行レベルは、ドライバーの i/o 要求を処理するオブジェクトのイベントコールバック関数をフレームワークが呼び出す IRQL を指定します。

ドライバーが実行レベルを提供する場合、指定されたレベルはキューおよびファイルオブジェクトのコールバック関数に影響します。 通常、ドライバーが自動同期を使用している場合、フレームワークは、IRQL = ディスパッチ\_レベルでこれらのコールバック関数を呼び出します。 実行レベルを指定することにより、ドライバーは、IRQL = パッシブ\_レベルでこれらのコールバック関数を呼び出すようにフレームワークに強制できます。 キューおよびファイルオブジェクトのコールバック関数が呼び出される IRQL を設定するときに、フレームワークは次の規則を使用します。

-   ドライバーが自動同期を使用する場合、ドライバーが IRQL = パッシブ\_レベルでコールバック関数を呼び出すように要求しない限り、そのキューおよびファイルオブジェクトのコールバック関数は IRQL = ディスパッチ\_レベルで呼び出されます。

-   ドライバーが自動同期を使用せず、実行レベルが指定されていない場合は、ドライバーの queue および file オブジェクトコールバック関数を IRQL &lt;= DISPATCH\_レベルで呼び出すことができます。

ドライバーにファイルオブジェクトのコールバック関数が用意されている場合、ファイル名などの一部のファイルデータはページング可能であるため、ほとんどの場合、これらのコールバック関数を IRQL = パッシブ\_レベルで呼び出す必要があります。

実行レベルを指定するには、ドライバーでオブジェクトの[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造体の**executionlevel**メンバーの値を指定する必要があります。 ドライバーが指定できる実行レベルの値は次のとおりです。

<a href="" id="wdfexecutionlevelpassive"></a>**WdfExecutionLevelPassive**  
このフレームワークは、IRQL = パッシブ\_レベルでオブジェクトのコールバック関数を呼び出します。

<a href="" id="wdfexecutionleveldispatch"></a>**WdfExecutionLevelDispatch**  
このフレームワークは、オブジェクトのコールバック関数を IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。 (ドライバーが自動同期を使用している場合、フレームワークは常に、IRQL = ディスパッチ\_レベルでコールバック関数を呼び出します)。

<a href="" id="wdfexecutionlevelinheritfromparent"></a>**WdfExecutionLevelInheritFromParent**  
フレームワークは、オブジェクトの親からオブジェクトの**Executionlevel**の値を取得します。

ドライバーオブジェクトの既定の実行レベルは、 **Wdfexecutionleveldispatch**です。 他のすべてのオブジェクトの既定の実行レベルは、 **Wdfexecutionlevelinheritfromparent**です。

実行レベルの値の詳細については、「 [**WDF\_execution\_level**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ne-wdfobject-_wdf_execution_level)」を参照してください。

次の表は、キューオブジェクトとファイルオブジェクトに対して、フレームワークがドライバーのコールバック関数を呼び出すことができる IRQL レベルを示しています。

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
<th align="left">キューとファイルのコールバック関数の IRQL</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Wdf同期スコープデバイス</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Wdf同期スコープデバイス</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelDispatch</strong></p></td>
<td align="left"><p>DISPATCH_LEVEL</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Wdf同期 Scopequeue</strong></p></td>
<td align="left"><p><strong>WdfExecutionLevelPassive</strong></p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Wdf同期 Scopequeue</strong></p></td>
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

 

ドライバー、デバイス、ファイル、キュー、タイマー、および一般的なオブジェクトに対して、実行レベルを**Wdfexecutionlevelpassive**または**Wdfexecutionlevelpassive**に設定できます。 他のオブジェクトの場合は、 **Wdfexecutionlevelinheritfromparent**だけを使用できます。

次の場合は、 **Wdfexecutionlevelpassive**を指定する必要があります。

-   ドライバーのコールバック関数は、IRQL = パッシブ\_レベルでのみ呼び出すことができるフレームワークメソッドまたは Windows Driver Model (WDM) ルーチンを呼び出す必要があります。

-   ドライバーのコールバック関数は、ページング可能なコードまたはデータにアクセスする必要があります。 (たとえば、ファイルオブジェクトのコールバック関数は、通常はページング可能なデータにアクセスします)。

**Wdfexecutionlevelpassive**を設定する代わりに、ドライバーは**Wdfexecutionlevelpassive**を設定し、IRQL = パッシブ\_レベルで一部の操作を処理する必要がある場合に[作業項目](using-framework-work-items.md)を作成するコールバック関数を提供することができます。

ドライバーがオブジェクトの実行レベルを**Wdfexecutionlevelpassive**に設定する必要があるかどうかを判断する前に、ドライバースタック内のドライバーおよびその他のドライバーが呼び出される IRQL を決定する必要があります。 次のような状況が考えられます。

-   ドライバーがカーネルモードドライバースタックの最上位にある場合、システムは通常、IRQL = パッシブ\_レベルでドライバーを呼び出します。 このようなドライバーのクライアントは、UMDF ベースのドライバーまたはユーザーモードアプリケーションである可能性があります。 **Wdfexecutionlevelpassive**を指定すると、ドライバーのパフォーマンスに悪影響を与えることはありません。これは、IRQL = パッシブ\_レベルで呼び出される作業項目へのドライバーの呼び出しをフレームワークがキューに含める必要がないためです。

-   ドライバーがスタックの一番上にない場合、システムは IRQL = パッシブ\_レベルではドライバーを呼び出さない可能性があります。 したがって、フレームワークは、後で IRQL = パッシブ\_レベルで呼び出される作業項目へのドライバーの呼び出しをキューに置いている必要があります。 このプロセスでは、ドライバーのコールバック関数を IRQL &lt;= DISPATCH\_レベルで呼び出すことができるのと比較して、ドライバーのパフォーマンスが低下する可能性があります。

DPC オブジェクト、および[パッシブレベルのタイマー](using-timers.md)を表さないタイマーオブジェクトの場合、親デバイスの実行レベルを設定している場合は、構成構造の自動**シリアル化**メンバーを**TRUE**に設定できないことに注意してください。を**Wdfexecutionlevelpassive**にします。 これは、フレームワークは、IRQL = パッシブ\_レベルでデバイスオブジェクトの[コールバック同期ロック](using-framework-locks.md)を取得するためです。そのため、DPC またはタイマーオブジェクトのコールバック関数を同期するためにロックを使用することはできませんが、irql =\_レベルをディスパッチします。 このような場合、ドライバーは、相互に同期する必要があるすべてのデバイス、DPC、またはタイマーオブジェクトのコールバック関数で、[フレームワークのスピンロック](using-framework-locks.md#framework-spin-locks)を使用する必要があります。

また、パッシブレベルのタイマーを*表すタイマーオブジェクトでは*、親デバイスの実行レベルが**Wdfexecutionlevelpassive**に設定されている場合に*のみ*、構成構造の自動**シリアル化**メンバーを TRUE に設定できます。

 

 





