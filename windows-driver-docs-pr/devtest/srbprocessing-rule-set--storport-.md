---
title: SrbProcessing の規則セット (Storport)
description: ドライバーが正しく SRB の要求を処理することを確認するのにには、これらの規則を使用します。
ms.assetid: A3BF2AA3-207F-4D74-94B0-6CA215341340
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9c895ca011b7c42cacaa232aa74867a1af618c5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349111"
---
# <a name="srbprocessing-rule-set-storport"></a>SrbProcessing の規則セット (Storport)


ドライバーが正しく SRB の要求を処理することを確認するのにには、これらの規則を使用します。

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
<td align="left"><p><a href="storport-spduplex.md" data-raw-source="[&lt;strong&gt;SpDuplex&lt;/strong&gt;](storport-spduplex.md)"><strong>SpDuplex</strong></a></p></td>
<td align="left"><p>このルールは、このミニポートことを確認します。<strong>全二重</strong>モード。 すべてのドライバー、StorPort ミニポート モデルに基づいて構築されていますがである必要があります<strong>全二重</strong>モード。 <strong>半二重</strong>StorPort を既存の SCSI ドライバーを移植するときにのみ使用する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spnowait.md" data-raw-source="[&lt;strong&gt;SpNoWait&lt;/strong&gt;](storport-spnowait.md)"><strong>SpNoWait</strong></a></p></td>
<td align="left"><p>このルールは、待機、またはデータの割り当ては内で実行していないことを検証<strong>StartIo</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spreturnvalue.md" data-raw-source="[&lt;strong&gt;SpReturnValue&lt;/strong&gt;](storport-spreturnvalue.md)"><strong>SpReturnValue</strong></a></p></td>
<td align="left"><p>このルールを検証するドライバーの実装の<a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557390)"> <strong>HwStorFindAdapter</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff568008" data-raw-source="[&lt;strong&gt;VirtualHwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568008)"> <strong>VirtualHwStorFindAdapter</strong> </a>返す有効な状態です。 有効な状態は、次のいずれか。<strong>SP_RETURN_FOUND</strong>、 <strong>SP_RETURN_ERROR</strong>、 <strong>SP_RETURN_BAD_CONFIG</strong>、または<strong>SP_RETURN_NOT_FOUND</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storportallocatepool.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](storportallocatepool.md)"><strong>StorPortAllocatePool</strong></a></p></td>
<td align="left"><p>このルールは、ミニポートが呼び出しを試みる必要がありますいないを確認します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567065" data-raw-source="[&lt;strong&gt;StorPortFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567065)"> <strong>StorPortFreePool</strong> </a> 、割り当てが解除されたバッファーにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportallocatepool2.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool2&lt;/strong&gt;](storport-storportallocatepool2.md)"><strong>StorPortAllocatePool2</strong></a></p></td>
<td align="left"><p>このルールは、ミニポートが呼び出しを試みる必要がありますいないを確認します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567031" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567031)"> <strong>StorPortAllocatePool</strong> </a>で最初に割り当てを解除せず、割り当てられたバッファー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"><strong>StorPortBuildIo</strong></a></p></td>
<td align="left"><p>このルールを検証する場合、StorPort ミニポートの<a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"> <strong>StorPortBuildIo</strong> </a>ルーチンを返します<strong>FALSE</strong>、問題の SRB はに渡されません<strong>StartIo</strong>。 (このような場合は、ミニポート ドライバーは、呼び出すことによって、SRB を完了する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff567433" data-raw-source="[&lt;strong&gt;StorPortNotification&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567433)"> <strong>StorPortNotification</strong> </a>の通知の種類と<strong>RequestComplete</strong>から<strong>StorPortBuildIo</strong>またはその他の場所)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportcompleterequest.md" data-raw-source="[&lt;strong&gt;StorPortCompleteRequest&lt;/strong&gt;](storport-storportcompleterequest.md)"><strong>StorPortCompleteRequest</strong></a></p></td>
<td align="left"><p>このルールを確認するを呼び出せなく<strong>StorPortCompleteRequest</strong>ミニポートによって行われます。 使用状況、 <strong>StorPortCompleteRequest</strong>は推奨されません。 ミニポートが代わりに呼び出す必要があります<strong>StorPortNotification</strong>で<strong>notificationType = RequestComplete</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportenablepassive.md" data-raw-source="[&lt;strong&gt;StorPortEnablePassive&lt;/strong&gt;](storport-storportenablepassive.md)"><strong>StorPortEnablePassive</strong></a></p></td>
<td align="left"><p>このルールはことを確認します<strong>StorPortEnablePassiveInitialization</strong>からは呼び出されません、StorPort ミニポート ドライバー ルーチン以外<strong>HwInitialize</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportfindadapter.md" data-raw-source="[&lt;strong&gt;StorPortFindAdapter&lt;/strong&gt;](storport-storportfindadapter.md)"><strong>StorPortFindAdapter</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557390" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557390)"> <strong>HwStorFindAdapter</strong> </a>ルーチンを設定する必要があります、 <strong>MaximumTransferLength</strong>と<strong>NumberOfPhysicalBreaks</strong> 内のフィールド<strong>PORT_CONFIGURATION_INFORMATION</strong>構造体。 これら両方のフィールドの値は、既定では、 <strong>SP_UNINITIALIZED_VALUE</strong>します。 これらのフィールドのいずれかに設定されたままの場合<strong>SP_UNINITIALIZED_VALUE</strong>から終了時に<strong>FindAdapter</strong>ドライバーが、規則に失敗します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportnotification2.md" data-raw-source="[&lt;strong&gt;StorPortNotification2&lt;/strong&gt;](storport-storportnotification2.md)"><strong>StorPortNotification2</strong></a></p></td>
<td align="left"><p>このルールへの呼び出しを検証<strong>StorPortNotification</strong>のみ使用できます (つまり文書化された) 通知の種類を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportpassivefromhwinit.md" data-raw-source="[&lt;strong&gt;StorPortPassiveFromHwInit&lt;/strong&gt;](storport-storportpassivefromhwinit.md)"><strong>StorPortPassiveFromHwInit</strong></a></p></td>
<td align="left"><p><strong>StorPortEnablePassiveInitialization</strong>呼び出すことはできません HW 初期化のエントリ ポイント内で Storport ドライバーの場合は、ハードウェアの初期化のエントリ ポイントをハードウェア アダプターのコントロールのエントリ ポイントから直接呼び出すことができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportperfopts.md" data-raw-source="[&lt;strong&gt;StorPortPerfOpts&lt;/strong&gt;](storport-storportperfopts.md)"><strong>StorPortPerfOpts</strong></a></p></td>
<td align="left"><p>このルールは、ことを確認、 <strong>PerfConfigData</strong>パラメーターに渡される<strong>StorPortInitializePerfOpts</strong>が NULL でないです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportstartio.md" data-raw-source="[&lt;strong&gt;StorPortStartIo&lt;/strong&gt;](storport-storportstartio.md)"><strong>StorPortStartIo</strong></a></p></td>
<td align="left"><p>待機またはデータ割り当てする必要があります、ミニポートのでは実行しないで<strong>StartIo</strong>ルーチン。 呼び出す場合、ドライバーは、ルールが失敗した<strong>StorPortStallExecution</strong>または時間のかかる操作を含む別の関数。 <strong>StartIo</strong>が同期されると、これらの呼び出しはほとんどの場合で行う<strong>BuildIo</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storporttimer.md" data-raw-source="[&lt;strong&gt;StorPortTimer&lt;/strong&gt;](storport-storporttimer.md)"><strong>StorPortTimer</strong></a></p></td>
<td align="left"><p><strong>HW_TIMER</strong>への呼び出し、ルーチンを定義する必要があります<strong>StorPortNotification(RequestTimerCall)</strong>されます。</p></td>
</tr>
</tbody>
</table>

 

**SrbProcessing ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **SrbProcessing**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **SrbProcessing.sdv**で、 **/check**オプション。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:SrbProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 





