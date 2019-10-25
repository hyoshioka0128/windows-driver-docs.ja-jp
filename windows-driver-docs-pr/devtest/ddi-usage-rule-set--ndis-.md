---
title: DDI 使用の規則セット (NDIS)
description: これらのルールを使用して、ドライバーが NDIS DDIs を正しく使用していることを確認します。
ms.assetid: A109A452-D3A7-4204-B267-1F0F98652597
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2e005c82b430068e8c66d0243d5dac296a7d5799
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839573"
---
# <a name="ddi-usage-rule-set-ndis"></a>DDI 使用の規則セット (NDIS)


これらのルールを使用して、ドライバーが NDIS DDIs を正しく使用していることを確認します。

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
<td align="left"><p><a href="ndis-init-deregisterinterrupt.md" data-raw-source="[&lt;strong&gt;Init_DeRegisterInterrupt&lt;/strong&gt;](ndis-init-deregisterinterrupt.md)"><strong>Init_DeRegisterInterrupt</strong></a></p></td>
<td align="left"><p><a href="ndis-init-deregisterinterrupt.md" data-raw-source="[&lt;strong&gt;Init_DeRegisterInterrupt&lt;/strong&gt;](ndis-init-deregisterinterrupt.md)"><strong>Init_DeRegisterInterrupt</strong></a>ルールでは、MPInitilize 中に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex" data-raw-source="[&lt;strong&gt;NdisMRegisterInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)"><strong>NdisMRegisterInterruptEx</strong></a>が少なくとも1回呼び出された場合、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)"><strong>NdisMDeregisterInterruptEx</strong></a>は MPHaltEx で少なくとも1回呼び出される必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"><strong>Init_NdisAllocateIoWorkItem</strong></a></p></td>
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"><strong>Init_NdisAllocateIoWorkItem</strong></a>ルールでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a>中に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem" data-raw-source="[&lt;strong&gt;NdisAllocateIoWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocateioworkitem)"><strong>NdisAllocateIoWorkItem</strong></a>が少なくとも1回呼び出されると、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem" data-raw-source="[&lt;strong&gt;NdisFreeIoWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreeioworkitem)"><strong>NdisFreeIoWorkItem</strong></a>関数は次のことを行う必要があることを指定します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a>が成功した場合は、MPHaltEx で少なくとも1回は呼び出されます。 -</li>
<li><em>MiniportInitializeEx</em>が失敗した場合は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)"><em>MiniportInitializeEx</em></a>で呼び出さ - ます。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-init-registerinterrupt.md" data-raw-source="[&lt;strong&gt;Init_RegisterInterrupt&lt;/strong&gt;](ndis-init-registerinterrupt.md)"><strong>Init_RegisterInterrupt</strong></a></p></td>
<td align="left"><p>Init_RegisterInterrupt 規則は、初期化プロセスで何らかの問題が発生した場合、またはミニポートドライバーの停止時に、通常は初期化中に発生する割り込みの登録を元に戻す必要があることを指定します。</p>
<p><strong>NdisMRegisterInterruptEx</strong>が<strong>MiniportInitializeEx</strong>中に少なくとも1回呼び出される場合は、 <strong>NdisMDeregisterInterruptEx</strong>関数を<strong>miniporthaltex</strong>で少なくとも1回呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-registersg.md" data-raw-source="[&lt;strong&gt;Init_RegisterSG&lt;/strong&gt;](ndis-init-registersg.md)"><strong>Init_RegisterSG</strong></a></p></td>
<td align="left"><p>Init_RegisterSG 規則は、初期化プロセスで何らかの問題が発生した場合、またはミニポートドライバーの停止時に、通常は初期化中に発生するスキャッター/ギャザーリスト (SG) の登録を元に戻す必要があることを指定します。</p>
<p><strong>MiniportInitializeEx</strong>中に<strong>NdisMRegisterScatterGatherDma</strong>が少なくとも1回呼び出された場合は、 <strong>NdisMDeregisterScatterGatherDma</strong>関数を<strong>miniporthaltex</strong>で少なくとも1回呼び出す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisfderegisterfilterdriver.md" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](ndis-ndisfderegisterfilterdriver.md)"><strong>NdisFDeregisterFilterDriver</strong></a></p></td>
<td align="left"><p>フィルタードライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/unloading-a-filter-driver" data-raw-source="[&lt;strong&gt;FilterDriverUnload&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/unloading-a-filter-driver)"><strong>Filterdriverunload</strong></a>ルーチンから<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)"><strong>NdisFDeregisterFilterDriver</strong></a>を呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismderegisterinterruptex.md" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](ndis-ndismderegisterinterruptex.md)"><strong>NdisMDeregisterInterruptEx</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)"><strong>NdisMDeregisterInterruptEx</strong></a>が制御を返すと、ミニポートドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex" data-raw-source="[&lt;strong&gt;NdisMSynchronizeWithInterruptEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsynchronizewithinterruptex)"><strong>NdisMSynchronizeWithInterruptEx</strong></a>関数を呼び出すことができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="nullcheckn.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckn.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck 規則は、ドライバーコード内の NULL 値がドライバーの後で逆参照されないことを検証します。 このルールは、次のいずれかの条件が満たされた場合に、欠陥を報告します。</p>
<ul>
<li>後で逆参照される NULL の割り当てがあります。</li>
<li>ドライバー内のプロシージャには、後で逆参照される可能性のあるグローバル/パラメーターがあります。また、ドライバーに明示的なチェックがあり、ポインターの初期値が NULL である可能性があることが示されています。</li>
</ul>
<p>NullCheck 規則違反では、最も関連性の高いコードステートメントが [トレースツリー] ウィンドウで強調表示されます。 レポート出力の操作の詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report" data-raw-source="[Static Driver Verifier Report](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier-report)">静的ドライバーの検証ツールレポート</a>」と「<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer" data-raw-source="[Understanding the Trace Viewer](https://docs.microsoft.com/windows-hardware/drivers/devtest/understanding-the-defect-viewer)">トレースビューアーに</a>ついて」を参照してください。</p>
<p></p></td>
</tr>
</tbody>
</table>

 

**DDI 使用規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[規則セット]** で **[ddiusage]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**ddiusage. sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





