---
title: その他の規則セット (NDIS)
description: これらの規則を使用して、ドライバーがタイマー、一時停止操作、キー、文字列、およびバインドを適切に処理するための一般的な要件のセットに正しく従っていることを確認します。
ms.assetid: 2F4A68DB-7619-4F36-8FA1-C9350604FDED
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4feef80619a397d97221f2756d368563e8387b6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840123"
---
# <a name="miscellaneous-rule-set-ndis"></a>その他の規則セット (NDIS)


これらの規則を使用して、ドライバーがタイマー、一時停止操作、キー、文字列、およびバインドを適切に処理するための一般的な要件のセットに正しく従っていることを確認します。

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
<td align="left"><p><a href="ndis-canceltimerobject.md" data-raw-source="[&lt;strong&gt;CancelTimerObject&lt;/strong&gt;](ndis-canceltimerobject.md)"><strong>Canceltimerobject</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)"><strong>NdisSetTimerObject</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)"><strong>NdisCancelTimerObject</strong></a>が別の順序で呼び出されることを指定します。 究極の目標は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>Miniporthaltex</em></a>が終了したときにすべてのタイマーがキャンセルされるようにすることです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"><strong>MiniportPause_Return</strong></a></p></td>
<td align="left"><p><a href="ndis-miniportpause-return.md" data-raw-source="[&lt;strong&gt;MiniportPause_Return&lt;/strong&gt;](ndis-miniportpause-return.md)"><strong>MiniportPause_Return</strong></a>ルールでは、一時停止操作が完了した場合は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause" data-raw-source="[&lt;em&gt;MiniportPause&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)"><em>miniportpause</em></a>コールバック関数が NDIS_STATUS_SUCCESS のみを返すように指定します。または、ミニポートドライバーが一時停止状態にある場合は NDIS_STATUS_PENDING を返します。 返されたその他の状態は無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisopenconfigurationex.md" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](ndis-ndisopenconfigurationex.md)"><strong>NdisOpenConfigurationEx</strong></a></p></td>
<td align="left"><p>このルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex" data-raw-source="[&lt;strong&gt;NdisOpenConfigurationEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)"><strong>NdisOpenConfigurationEx</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration" data-raw-source="[&lt;strong&gt;NdisCloseConfiguration&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseconfiguration)"><strong>NdisCloseConfiguration</strong></a>が別の順序で呼び出されることを確認します。 究極の目標は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)"><em>Miniporthaltex</em></a>が終了したときに構成ハンドルが閉じられるようにすることです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisquerybindinstancename.md" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](ndis-ndisquerybindinstancename.md)"><strong>NdisQueryBindInstanceName</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerybindinstancename" data-raw-source="[&lt;strong&gt;NdisQueryBindInstanceName&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisquerybindinstancename)"><strong>NdisQueryBindInstanceName</strong></a>は、フレンドリ名を指定する文字列のメモリを割り当てます。 呼び出し元がこのメモリを使用して終了した後、呼び出し元は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory" data-raw-source="[&lt;strong&gt;NdisFreeMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreememory)"><strong>NdisFreeMemory</strong></a>関数を呼び出してメモリを解放する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisreenumerateprotocolbindings.md" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](ndis-ndisreenumerateprotocolbindings.md)"><strong>NdisReEnumerateProtocolBindings</strong></a></p></td>
<td align="left"><p>プロトコルドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolBindAdapterEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)"><em>protocolbindadapterex</em></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex" data-raw-source="[&lt;em&gt;ProtocolUnbindAdapterEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)"><em>protocolunbindadapterex</em></a>関数のコンテキスト内から<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings" data-raw-source="[&lt;strong&gt;NdisReEnumerateProtocolBindings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreenumerateprotocolbindings)"><strong>NdisReEnumerateProtocolBindings</strong></a>を呼び出すことはできません。 また、 <em>ProtocolNetPnPEvent</em>の<em>PROTOCOLBINDINGCONTEXT</em>パラメーターが NULL でない場合、プロトコルドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event" data-raw-source="[&lt;em&gt;ProtocolNetPnPEvent&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)"><em>ProtocolNetPnPEvent</em></a>関数のコンテキスト内から<strong>NdisReEnumerateProtocolBindings</strong>を呼び出すことができません。 ただし、 <em>ProtocolBindingContext</em>が NULL の場合、プロトコルドライバーは<em>ProtocolNetPnPEvent</em>のコンテキスト内から<strong>NdisReEnumerateProtocolBindings</strong>を呼び出すことができます。 NULL <em>ProtocolBindingContext</em>値は、イベントがすべてのバインドに適用されることを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"><strong>PeriodicTimer</strong></a></p></td>
<td align="left"><p>NdisCancelTimerObject の<em>MillisecondsPeriod</em>パラメーターに0以外の値が指定されている場合、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject" data-raw-source="[&lt;strong&gt;NdisCancelTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscanceltimerobject)"></a>の呼び出し元が<strong>IRQL = PASSIVE_LEVEL</strong>で実行され<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject" data-raw-source="[&lt;strong&gt;NdisSetTimerObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissettimerobject)"></a>ている必要があることを指定<a href="ndis-periodictimer.md" data-raw-source="[&lt;strong&gt;PeriodicTimer&lt;/strong&gt;](ndis-periodictimer.md)"><strong>します。</strong></a>プロシージャ. <strong>NdisSetTimerObject</strong>関数の<em>MillisecondsPeriod</em>パラメーターが0の場合、 <strong>NdisCancelTimerObject</strong>の呼び出し元は<strong>IRQL &lt;= DISPATCH_LEVEL</strong>で実行できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-writeerrorlog.md" data-raw-source="[&lt;strong&gt;WriteErrorLog&lt;/strong&gt;](ndis-writeerrorlog.md)"><strong>WriteErrorLog ログ</strong></a></p></td>
<td align="left"><p>WriteErrorLog ルールでは、 <em>MiniportInitializeEx</em>関数で<strong>NdisMAllocateSharedMemory</strong>関数が呼び出された場合、ドライバーは、割り当てが失敗した場合に<strong>NdisWriteErrorLogEntry</strong>も呼び出す必要があることを指定します。</p></td>
</tr>
</tbody>
</table>

 

**その他のルールセットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[その他]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを使用して、**その他の sdv**を指定します。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:Miscellaneous.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





