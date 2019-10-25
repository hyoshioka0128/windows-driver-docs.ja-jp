---
title: SrbProcessing ルールセット (Storport)
description: これらのルールを使用して、ドライバーが SRB 要求を正しく処理していることを確認します。
ms.assetid: A3BF2AA3-207F-4D74-94B0-6CA215341340
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: f82071e196be56f3230c551042c4966b31de6597
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839321"
---
# <a name="srbprocessing-rule-set-storport"></a>SrbProcessing ルールセット (Storport)


これらのルールを使用して、ドライバーが SRB 要求を正しく処理していることを確認します。

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
<td align="left"><p>このルールは、このミニポートが<strong>全二重</strong>モードであることを確認します。 StorPort ミニポートモデルに従って構築されたドライバーは、<strong>全二重</strong>モードである必要があります。 既存の SCSI ドライバーを StorPort に移植する場合にのみ、<strong>半二重</strong>を使用する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-spnowait.md" data-raw-source="[&lt;strong&gt;SpNoWait&lt;/strong&gt;](storport-spnowait.md)"><strong>SpNoWait</strong></a></p></td>
<td align="left"><p>このルールは、待機またはデータ割り当てが<strong>StartIo</strong>内で実行されないことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-spreturnvalue.md" data-raw-source="[&lt;strong&gt;SpReturnValue&lt;/strong&gt;](storport-spreturnvalue.md)"><strong>SpReturnValue</strong></a></p></td>
<td align="left"><p>このルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter" data-raw-source="[&lt;strong&gt;VirtualHwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-virtual_hw_find_adapter)"><strong>VirtualHwStorFindAdapter</strong></a>のドライバーの実装が有効な状態を返すことを確認します。 有効な状態は次のいずれかです: <strong>SP_RETURN_FOUND</strong>、 <strong>SP_RETURN_ERROR</strong>、 <strong>SP_RETURN_BAD_CONFIG</strong>、または<strong>SP_RETURN_NOT_FOUND</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storportallocatepool.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](storportallocatepool.md)"><strong>StorPortAllocatePool</strong></a></p></td>
<td align="left"><p>このルールは、割り当て解除されたバッファーで、ミニポートが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool" data-raw-source="[&lt;strong&gt;StorPortFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool)"><strong>Storportfreepool</strong></a>を呼び出すことができないことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportallocatepool2.md" data-raw-source="[&lt;strong&gt;StorPortAllocatePool2&lt;/strong&gt;](storport-storportallocatepool2.md)"><strong>StorPortAllocatePool2</strong></a></p></td>
<td align="left"><p>このルールは、割り当てられたバッファーに対して、最初に割り当て解除せずに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool" data-raw-source="[&lt;strong&gt;StorPortAllocatePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool)"><strong>StorPortAllocatePool</strong></a>を呼び出すことができないことを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"><strong>StorPortBuildIo</strong></a></p></td>
<td align="left"><p>このルールは、StorPort ミニポートの<a href="storport-storportbuildio.md" data-raw-source="[&lt;strong&gt;StorPortBuildIo&lt;/strong&gt;](storport-storportbuildio.md)"><strong>StorPortBuildIo</strong></a>ルーチンから<strong>FALSE</strong>が返された場合に、該当する SRB が<strong>StartIo</strong>に渡されないことを確認します。 (このような場合、ミニポートドライバーは、 <strong>StorPortBuildIo</strong>または他の場所からの<strong>requestcomplete</strong>の通知の種類で<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification" data-raw-source="[&lt;strong&gt;StorPortNotification&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)"><strong>storportnotification</strong></a>を呼び出すことによって、SRB を完了する必要があります)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportcompleterequest.md" data-raw-source="[&lt;strong&gt;StorPortCompleteRequest&lt;/strong&gt;](storport-storportcompleterequest.md)"><strong>StorPortCompleteRequest</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>StorPortCompleteRequest</strong>への呼び出しがミニポートによって行われていないことを確認します。 <strong>StorPortCompleteRequest</strong>の使用は推奨されません。ミニポートは、代わりに<strong>notificationType = RequestComplete</strong>で<strong>storportnotification</strong>を呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportenablepassive.md" data-raw-source="[&lt;strong&gt;StorPortEnablePassive&lt;/strong&gt;](storport-storportenablepassive.md)"><strong>StorPortEnablePassive</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>HwInitialize</strong>以外の StorPort ミニポートドライバールーチンから<strong>Storportenable veinitialization</strong>が呼び出されないことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportfindadapter.md" data-raw-source="[&lt;strong&gt;StorPortFindAdapter&lt;/strong&gt;](storport-storportfindadapter.md)"><strong>StorPortFindAdapter</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>ルーチンでは、 <strong>PORT_CONFIGURATION_INFORMATION</strong>構造体の<strong>Maximumtransferlength</strong>フィールドと<strong>numberofphysicalbreaks</strong>フィールドを設定する必要があります。 既定では、両方のフィールドの値は<strong>SP_UNINITIALIZED_VALUE</strong>です。 これらのフィールドのいずれかが、 <strong>Findadapter</strong>からの終了時に<strong>SP_UNINITIALIZED_VALUE</strong>に設定されている場合、ドライバーはルールに失敗します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportnotification2.md" data-raw-source="[&lt;strong&gt;StorPortNotification2&lt;/strong&gt;](storport-storportnotification2.md)"><strong>StorPortNotification2</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>Storportnotification</strong>への呼び出しで許可されている (つまり、ドキュメント化された) 通知の種類のみを使用することを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportpassivefromhwinit.md" data-raw-source="[&lt;strong&gt;StorPortPassiveFromHwInit&lt;/strong&gt;](storport-storportpassivefromhwinit.md)"><strong>Storport"Vefromhwinit"</strong></a></p></td>
<td align="left"><p>Hw 初期化エントリポイントを HW アダプターコントロールのエントリポイントから直接呼び出すことができる場合、Storport ドライバーの HW 初期化エントリポイント内で<strong>Storportenableの Veinitialization</strong>を呼び出すことはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storportperfopts.md" data-raw-source="[&lt;strong&gt;StorPortPerfOpts&lt;/strong&gt;](storport-storportperfopts.md)"><strong>StorPortPerfOpts</strong></a></p></td>
<td align="left"><p>このルールは、 <strong>Storportinitializeperfopts</strong>渡される<strong>perfconfigdata</strong>パラメーターが NULL でないことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="storport-storportstartio.md" data-raw-source="[&lt;strong&gt;StorPortStartIo&lt;/strong&gt;](storport-storportstartio.md)"><strong>StorPortStartIo</strong></a></p></td>
<td align="left"><p>待機またはデータ割り当てをミニポートの<strong>StartIo</strong>ルーチンで実行することはできません。 ドライブが<strong>Storportstallexecution</strong>を呼び出した場合、または時間のかかる操作を伴う別の関数を呼び出した場合、このルールは失敗します。 <strong>StartIo</strong>は同期されるため、これらの呼び出しは、ほとんどの場合、 <strong>BuildIo</strong>で実行する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="storport-storporttimer.md" data-raw-source="[&lt;strong&gt;StorPortTimer&lt;/strong&gt;](storport-storporttimer.md)"><strong>StorPortTimer</strong></a></p></td>
<td align="left"><p><strong>Storportnotification (RequestTimerCall)</strong>の呼び出しが行われた場合は、 <strong>HW_TIMER</strong>ルーチンを定義する必要があります。</p></td>
</tr>
</tbody>
</table>

 

**SrbProcessing ルールセットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で、 **[srbprocessing]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**srbprocessing. sdv**を指定します。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:SrbProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





