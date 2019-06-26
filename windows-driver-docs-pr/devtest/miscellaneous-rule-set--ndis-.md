---
title: その他の規則セット (NDIS)
description: これらの規則を使用すると、タイマー、一時停止操作、キー、文字列、およびバインディングの適切な処理の要件の一般的なセットが正しくに、ドライバーに従うことを確認します。
ms.assetid: 2F4A68DB-7619-4F36-8FA1-C9350604FDED
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: adc285a3671287e2f85f232261e6d4ae762c42b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361296"
---
# <a name="miscellaneous-rule-set-ndis"></a>その他の規則セット (NDIS)


これらの規則を使用すると、タイマー、一時停止操作、キー、文字列、およびバインディングの適切な処理の要件の一般的なセットが正しくに、ドライバーに従うことを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-canceltimerobject.md" data-raw-source="[&lt;strong&gt;CancelTimerObject&lt;/strong&gt;](ndis-canceltimerobject.md)"><strong>CancelTimerObject</strong></a></p></td>
<td align="left"><p><a href="ndis-canceltimerobject.md" data-raw-source="[&lt;strong&gt;CancelTimerObject&lt;/strong&gt;](ndis-canceltimerobject.md)"> <strong>CancelTimerObject</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)"> <strong>NdisSetTimerObject</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)"> <strong>NdisCancelTimerObject</strong> </a>代替の順序で呼び出されます。 最終的な目標はすべてのタイマーが取り消されるかどうかを確認するときに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>が終了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"><strong>MiniportPause_Return</strong></a></p></td>
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"> <strong>MiniportPause_Return</strong> </a>ルールでは、ことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)"> <em>MiniportPause</em> </a>コールバック関数が NDIS_STATUS_ のみを返す必要があります一時停止操作が完了すると場合の成功または NDIS_STATUS_PENDING ミニポート ドライバーが一時停止状態にある場合。 返されるその他のすべての状態が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisopenconfigurationex.md" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](ndis-ndisopenconfigurationex.md)"><strong>NdisOpenConfigurationEx</strong></a></p></td>
<td align="left"><p>このルールは、ことを確認<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex)"> <strong>NdisOpenConfigurationEx</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseconfiguration" data-raw-source="[&lt;strong&gt;NdisCloseConfiguration&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseconfiguration)"> <strong>NdisCloseConfiguration</strong> </a>代替の順序で呼び出されます。 最終的な目標は、構成のハンドルが閉じられている場合にかどうかを確認する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>終了</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisquerybindinstancename.md" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](ndis-ndisquerybindinstancename.md)"><strong>NdisQueryBindInstanceName</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisquerybindinstancename" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisquerybindinstancename)"><strong>NdisQueryBindInstanceName</strong> </a>フレンドリ名を指定する文字列のメモリを割り当てます。 呼び出し元は、このメモリを使用して完了すると、呼び出し元が呼び出す必要があります、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory" data-raw-source="[&lt;strong&gt;NdisFreeMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreememory)"> <strong>NdisFreeMemory</strong> </a>関数にメモリを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisreenumerateprotocolbindings.md" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](ndis-ndisreenumerateprotocolbindings.md)"><strong>NdisReEnumerateProtocolBindings</strong></a></p></td>
<td align="left"><p>プロトコル ドライバーに呼び出すことはできません<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreenumerateprotocolbindings" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreenumerateprotocolbindings)"> <strong>NdisReEnumerateProtocolBindings</strong> </a>からのコンテキスト内で、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolBindAdapterEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)"> <em>ProtocolBindAdapterEx</em> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolUnbindAdapterEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)"> <em>ProtocolUnbindAdapterEx</em> </a>関数。 また、プロトコルのドライバーを呼び出すことはできません<strong>NdisReEnumerateProtocolBindings</strong>からのコンテキスト内で、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event" data-raw-source="[&lt;em&gt;ProtocolNetPnPEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)"> <em>ProtocolNetPnPEvent</em> </a>関数の場合、 <em>ProtocolBindingContext</em>パラメーターの<em>ProtocolNetPnPEvent</em>が NULL でないです。 ただし、プロトコルのドライバーを呼び出すことができます<strong>NdisReEnumerateProtocolBindings</strong>からのコンテキスト内で<em>ProtocolNetPnPEvent</em>場合<em>ProtocolBindingContext</em>は NULL です。 NULL <em>ProtocolBindingContext</em>値では、イベントがすべてのバインドに適用されることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"><strong>PeriodicTimer</strong></a></p></td>
<td align="left"><p><a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"> <strong>PeriodicTimer</strong> </a>ルールを指定する、呼び出し元の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscanceltimerobject)"> <strong>NdisCancelTimerObject</strong> </a>で実行する必要があります<strong>IRQL =PASSIVE_LEVEL</strong>で 0 以外の値が指定されている場合、 <em>MillisecondsPeriod</em>のパラメーター、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissettimerobject)"> <strong>NdisSetTimerObject</strong> </a>関数。 場合、 <em>MillisecondsPeriod</em>のパラメーター、 <strong>NdisSetTimerObject</strong>関数がゼロ、呼び出し元の<strong>NdisCancelTimerObject</strong>で実行されている<strong>IRQL&lt;= DISPATCH_LEVEL</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-writeerrorlog.md" data-raw-source="[&lt;strong&gt;WriteErrorLog&lt;/strong&gt;](ndis-writeerrorlog.md)"><strong>WriteErrorLog</strong></a></p></td>
<td align="left"><p>WriteErrorLog ルールで指定された場合、 <strong>NdisMAllocateSharedMemory</strong>関数が呼び出されます、 <em>MiniportInitializeEx</em>関数の場合、ドライバーは呼び出す必要がありますも<strong>NdisWriteErrorLogEntry</strong>割り当てに失敗した場合。</p></td>
</tr>
</tbody>
</table>

 

**その他のルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **その他**。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Miscellaneous.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





