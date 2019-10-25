---
title: IrpProcessing の規則セット (KMDF)
description: これらのルールを使用して、ドライバーが i/o 要求パケット (IRP) を正しく処理していることを確認します。
ms.assetid: B403F21E-FE35-4A57-92DB-C78FDC1488BD
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3167c18830eaee76975ec5136cfcafd7e42a6731
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839551"
---
# <a name="irpprocessing-rule-set-kmdf"></a>IrpProcessing の規則セット (KMDF)


これらのルールを使用して、ドライバーが i/o 要求パケット (IRP) を正しく処理していることを確認します。

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
<td align="left"><p><a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"><strong>FwdIrpToIoQueueValid</strong></a></p></td>
<td align="left"><p>ルール<a href="kmdf-fwdirptoioqueuevalid.md" data-raw-source="[&lt;strong&gt;FwdIrpToIoQueueValid&lt;/strong&gt;](kmdf-fwdirptoioqueuevalid.md)"><strong>FwdIrpToIoQueueValid</strong></a>は、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue" data-raw-source="[&lt;strong&gt;WdfDeviceWdmDispatchIrpToIoQueue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmdispatchirptoioqueue)"><strong>WdfDeviceWdmDispatchIrpToIoQueue</strong></a>メソッドを使用して、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)"><em>Evtdevicewdmi ディスパッチ</em></a>コールバックまたは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpPreprocess&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)"><em>evtdevicewdmiのプリプロセス</em></a>からの IRP を i/o キューに送信することを指定します。コール.</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"><strong>SetCompletionRoutineFromDispatch</strong></a></p></td>
<td align="left"><p><a href="kmdf-setcompletionroutinefromdispatch.md" data-raw-source="[&lt;strong&gt;SetCompletionRoutineFromDispatch&lt;/strong&gt;](kmdf-setcompletionroutinefromdispatch.md)"><strong>SetCompletionRoutineFromDispatch</strong></a>ルールは、ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch" data-raw-source="[&lt;em&gt;EvtDeviceWdmIrpDispatch&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_dispatch)"><em>Evtdevicewdmi ディスパッチ</em></a>コールバック関数からの IRP で完了ルーチンを指定していないことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"><strong>MiniportOnlyWdmDevice</strong></a></p></td>
<td align="left"><p><a href="kmdf-miniportonlywdmdevice.md" data-raw-source="[&lt;strong&gt;MiniportOnlyWdmDevice&lt;/strong&gt;](kmdf-miniportonlywdmdevice.md)"><strong>Miniportonlywdmdevice</strong></a>ルールでは、WDF ドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)"><strong>iocreate ec素</strong></a>関数を使用して、ベア WDM デバイスオブジェクトを作成しないように指定します。 これにより、他のユーザーが WDM デバイスに IRP を送信しようとすると、コンピューターがクラッシュします。 これは、デバイスの IRP ディスパッチエントリは WDF 固有のエントリに設定されていますが、フレームワークでは WDF デバイスが作成されていないためです。 ただし、ドライバーのディスパッチエントリポイントが設定されていないため、ミニポートドライバーは DDIs を使用できます。</p></td>
</tr>
</tbody>
</table>

 

**IrpProcessing 規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[ルールセット]** で **[irpprocessing]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して**irpprocessing. sdv**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:IrpProcessing.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





