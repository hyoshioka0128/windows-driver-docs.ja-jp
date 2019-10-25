---
title: Irql の規則セット (KMDF)
description: これらのルールを使用して、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。IRQL 規則に従っていないドライバーは、デッドロック状態またはコンピューターのクラッシュにつながる可能性がある操作中に重大な問題を引き起こす可能性があります。
ms.assetid: B02D196F-E8D5-4FE9-8983-AD08EAE00DE5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: b51d51661d66440bbd3e6245fdf8167870ce9dae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839547"
---
# <a name="irql-rule-set-kmdf"></a>Irql の規則セット (KMDF)


これらのルールを使用して、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。

IRQL 規則に従っていないドライバーは、デッドロック状態またはコンピューターのクラッシュにつながる可能性がある操作中に重大な問題を引き起こす可能性があります。

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
<td align="left"><p><a href="kmdf-kmdfirql.md" data-raw-source="[&lt;strong&gt;KmdfIrql&lt;/strong&gt;](kmdf-kmdfirql.md)"><strong>Kmdの Ql</strong></a></p></td>
<td align="left"><p><a href="kmdf-kmdfirql.md" data-raw-source="[&lt;strong&gt;KmdfIrql&lt;/strong&gt;](kmdf-kmdfirql.md)"><strong>Kmdno ql</strong></a>ルールは、ドライバーが、そのメソッドの最大 irql 以下の irql でフレームワークメソッドを呼び出すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-kmdfirql2.md" data-raw-source="[&lt;strong&gt;KmdfIrql2&lt;/strong&gt;](kmdf-kmdfirql2.md)"><strong>KmdfIrql2</strong></a></p></td>
<td align="left"><p><a href="kmdf-kmdfirql2.md" data-raw-source="[&lt;strong&gt;KmdfIrql2&lt;/strong&gt;](kmdf-kmdfirql2.md)"><strong>KmdfIrql2</strong></a>規則は、ドライバーが、そのメソッドの最大 irql 以下の irql でフレームワークメソッドを呼び出すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbkmdfirql.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql&lt;/strong&gt;](kmdf-usbkmdfirql.md)"><strong>Usbkmdファイヤ Ql</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbkmdfirql.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql&lt;/strong&gt;](kmdf-usbkmdfirql.md)"><strong>Usbkmdql ql</strong></a>ルールは、kmdf ドライバーが、正しくない IRQL レベルで USB 固有のデバイスドライバーインターフェイス (DDI) を呼び出さないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbkmdfirql2.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql2&lt;/strong&gt;](kmdf-usbkmdfirql2.md)"><strong>UsbKmdfIrql2</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbkmdfirql2.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql2&lt;/strong&gt;](kmdf-usbkmdfirql2.md)"><strong>UsbKmdfIrql2</strong></a>規則は、kmdf ドライバーが、正しくない IRQL レベルで USB 固有の DDIs を呼び出さないように指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="usbkmdfirqlexplicit.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrqlExplicit&lt;/strong&gt;](usbkmdfirqlexplicit.md)"><strong>Usbkmdの Qlexplicit</strong></a></p></td>
<td align="left"><p><a href="usbkmdfirqlexplicit.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrqlExplicit&lt;/strong&gt;](usbkmdfirqlexplicit.md)"><strong>Usbkmdの Qlexplicit</strong></a>ルールは、Kmdf DDIs が正しい IRQL レベルで呼び出されることを確認します。 このルールは、すべての EvtIoCallback 関数に適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdfrequestsendsyncatdispatch.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch&lt;/strong&gt;](wdfrequestsendsyncatdispatch.md)"><strong>WdfRequestSendSyncAtDispatch</strong></a></p></td>
<td align="left"><p><a href="wdfrequestsendsyncatdispatch.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch&lt;/strong&gt;](wdfrequestsendsyncatdispatch.md)"><strong>Wdfrequestsendsyncatdispatch</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>Wdfrequestsend</strong></a>関数が正しい IRQL 優先度レベルで送信されることを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdfrequestsendsyncatdispatch2.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch2&lt;/strong&gt;](wdfrequestsendsyncatdispatch2.md)"><strong>WdfRequestSendSyncAtDispatch2</strong></a></p></td>
<td align="left"><p><a href="wdfrequestsendsyncatdispatch2.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch2&lt;/strong&gt;](wdfrequestsendsyncatdispatch2.md)"><strong>WdfRequestSendSyncAtDispatch2</strong></a>ルールは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)"><strong>Wdfrequestsend</strong></a>関数が正しい IRQL 優先度レベルで送信されることを確認します。</p></td>
</tr>
</tbody>
</table>

 

**Irql 規則セットを選択するには**

1.  Microsoft Visual Studio でドライバープロジェクト (.Vcxproj) を選択します。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

2.  **[ルール]** タブをクリックします。 **[規則セット]** で **[Irql]** を選択します。

    Visual Studio 開発者コマンドプロンプトウィンドウから既定の規則セットを選択するには、 **/チェック**オプションを指定して、 **Irql**を指定します。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、「 [Using Static Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers) 」を参照して、ドライバーと[静的ドライバー検証コマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)で欠陥を検出してください。

 

 





