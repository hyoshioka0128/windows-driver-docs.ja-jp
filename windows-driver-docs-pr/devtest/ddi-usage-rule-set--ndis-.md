---
title: DDI 使用量ルール セット (NDIS)
description: これらの規則を使用すると、ドライバー、正しく使用する NDIS Ddi 正しくを確認します。
ms.assetid: A109A452-D3A7-4204-B267-1F0F98652597
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b6f876d189f9c83e274e16591aade6694eb24a3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527404"
---
# <a name="ddi-usage-rule-set-ndis"></a>DDI 使用量ルール セット (NDIS)


これらの規則を使用すると、ドライバー、正しく使用する NDIS Ddi 正しくを確認します。

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
<td align="left"><p><a href="ndis-init-deregisterinterrupt.md" data-raw-source="[&lt;strong&gt;Init_DeRegisterInterrupt&lt;/strong&gt;](ndis-init-deregisterinterrupt.md)"> <strong>Init_DeRegisterInterrupt</strong> </a>規則で指定された場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff563649" data-raw-source="[&lt;strong&gt;NdisMRegisterInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563649)"> <strong>NdisMRegisterInterruptEx</strong> </a>中に少なくとも 1 回呼び出されますMPInitilize、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563575" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563575)"> <strong>NdisMDeregisterInterruptEx</strong> </a> MPHaltEx で少なくとも 1 回呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"><strong>Init_NdisAllocateIoWorkItem</strong></a></p></td>
<td align="left"><p><a href="ndis-init-ndisallocateioworkitem.md" data-raw-source="[&lt;strong&gt;Init_NdisAllocateIoWorkItem&lt;/strong&gt;](ndis-init-ndisallocateioworkitem.md)"> <strong>Init_NdisAllocateIoWorkItem</strong> </a>規則で指定された場合<a href="https://msdn.microsoft.com/library/windows/hardware/ff561604" data-raw-source="[&lt;strong&gt;NdisAllocateIoWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561604)"> <strong>NdisAllocateIoWorkItem</strong> </a> 中に少なくとも1回呼び出されます<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"><em>MiniportInitializeEx</em></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff561855" data-raw-source="[&lt;strong&gt;NdisFreeIoWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561855)"> <strong>NdisFreeIoWorkItem</strong> </a>関数にする必要があります。</p>
<ul>
<li>- 場合に、MPHaltEx で少なくとも 1 回呼び出すこと<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"> <em>MiniportInitializeEx</em> </a>が成功するとします。</li>
<li>- 呼び出される<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"> <em>MiniportInitializeEx</em></a>場合は、 <em>MiniportInitializeEx</em>は失敗します。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-init-registerinterrupt.md" data-raw-source="[&lt;strong&gt;Init_RegisterInterrupt&lt;/strong&gt;](ndis-init-registerinterrupt.md)"><strong>Init_RegisterInterrupt</strong></a></p></td>
<td align="left"><p>Init_RegisterInterrupt ルールでは、ミニポート ドライバーが停止中または初期化プロセスで問題が発生した場合にする必要がありますの初期化中には、通常、割り込みの登録の元に戻すを解除することを指定します。</p>
<p>場合<strong>NdisMRegisterInterruptEx</strong>中に少なくとも 1 回と呼びます<strong>MiniportInitializeEx</strong>、 <strong>NdisMDeregisterInterruptEx</strong>関数は、少なくとも 1 回呼び出す必要があります<strong>MiniportHaltEx</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-init-registersg.md" data-raw-source="[&lt;strong&gt;Init_RegisterSG&lt;/strong&gt;](ndis-init-registersg.md)"><strong>Init_RegisterSG</strong></a></p></td>
<td align="left"><p>Init_RegisterSG ルールでは、ミニポート ドライバーが停止中または初期化プロセスで問題が発生した場合にする必要がありますの初期化中には、通常、スキャッター/ギャザー リスト (SG) の登録の元に戻すを解除することを指定します。</p>
<p>場合<strong>NdisMRegisterScatterGatherDma</strong>中に少なくとも 1 回と呼びます<strong>MiniportInitializeEx</strong>、 <strong>NdisMDeregisterScatterGatherDma</strong>で関数を呼び出す必要があります少なくとも 1 回<strong>MiniportHaltEx</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisfderegisterfilterdriver.md" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](ndis-ndisfderegisterfilterdriver.md)"><strong>NdisFDeregisterFilterDriver</strong></a></p></td>
<td align="left"><p>フィルター ドライバーを呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff561800" data-raw-source="[&lt;strong&gt;NdisFDeregisterFilterDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561800)"> <strong>NdisFDeregisterFilterDriver</strong> </a>からその<a href="https://msdn.microsoft.com/library/windows/hardware/ff549936" data-raw-source="[&lt;strong&gt;FilterDriverUnload&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549936)"> <strong>FilterDriverUnload</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismderegisterinterruptex.md" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](ndis-ndismderegisterinterruptex.md)"><strong>NdisMDeregisterInterruptEx</strong></a></p></td>
<td align="left"><p>後<a href="https://msdn.microsoft.com/library/windows/hardware/ff563575" data-raw-source="[&lt;strong&gt;NdisMDeregisterInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563575)"> <strong>NdisMDeregisterInterruptEx</strong> </a>コントロールを返します、ミニポート ドライバーを呼び出すことはできません、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff563681" data-raw-source="[&lt;strong&gt;NdisMSynchronizeWithInterruptEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563681)"> <strong>NdisMSynchronizeWithInterruptEx</strong> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="nullcheckn.md" data-raw-source="[&lt;strong&gt;NullCheck&lt;/strong&gt;](nullcheckn.md)"><strong>NullCheck</strong></a></p></td>
<td align="left"><p>NullCheck ルールは、ドライバーの後で、ドライバーのコード内の NULL 値が逆参照しないことを確認します。 このルールは、これらの条件のいずれかが true の場合、欠陥を報告します。</p>
<ul>
<li>以降は逆参照が NULL の代入です。</li>
<li>ドライバーでは、後で逆参照が NULL の可能性があるプロシージャにグローバル/パラメーターがあるし、ポインターの初期値は NULL である可能性がありますの候補を示す、ドライバーでの明示的なチェックがあります。</li>
</ul>
<p>NullCheck ルール違反では、最も関連のコード ステートメントは、トレースのツリー ペインで強調表示されます。 レポートの出力の使用方法の詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/ff552834" data-raw-source="[Static Driver Verifier Report](https://msdn.microsoft.com/library/windows/hardware/ff552834)">静的ドライバー検証ツールのレポート</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff554020" data-raw-source="[Understanding the Trace Viewer](https://msdn.microsoft.com/library/windows/hardware/ff554020)">トレース ビューアーを理解する</a>を参照してください。</p>
<p></p></td>
</tr>
</tbody>
</table>

 

**DDI 使用量のルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています.**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **DDIUsage**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **DDIUsage.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:DDIUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 





