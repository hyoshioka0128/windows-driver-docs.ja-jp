---
title: Irql の規則セット (KMDF)
description: これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。
ms.assetid: B02D196F-E8D5-4FE9-8983-AD08EAE00DE5
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a90f0200d22c637e361b0ae188b8283e86205b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373671"
---
# <a name="irql-rule-set-kmdf"></a>Irql の規則セット (KMDF)


これらの規則を使用すると、ドライバーが必要な IRQL で DDI 呼び出しを行うことを確認します。

IRQL の規則に従っていないドライバーは、デッドロック状態またはコンピューターがクラッシュする可能性のある操作中に重大な問題を発生することができます。

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
<td align="left"><p><a href="kmdf-kmdfirql.md" data-raw-source="[&lt;strong&gt;KmdfIrql&lt;/strong&gt;](kmdf-kmdfirql.md)"><strong>KmdfIrql</strong></a></p></td>
<td align="left"><p><a href="kmdf-kmdfirql.md" data-raw-source="[&lt;strong&gt;KmdfIrql&lt;/strong&gt;](kmdf-kmdfirql.md)"> <strong>KmdfIrql</strong> </a>ルールでは、ドライバーが、そのメソッドの最大の IRQL 小さい IRQL でフレームワーク メソッドを呼び出すことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-kmdfirql2.md" data-raw-source="[&lt;strong&gt;KmdfIrql2&lt;/strong&gt;](kmdf-kmdfirql2.md)"><strong>KmdfIrql2</strong></a></p></td>
<td align="left"><p><a href="kmdf-kmdfirql2.md" data-raw-source="[&lt;strong&gt;KmdfIrql2&lt;/strong&gt;](kmdf-kmdfirql2.md)"> <strong>KmdfIrql2</strong> </a>ルールでは、ドライバーが、そのメソッドの最大の IRQL 小さい IRQL でフレームワーク メソッドを呼び出すことを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="kmdf-usbkmdfirql.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql&lt;/strong&gt;](kmdf-usbkmdfirql.md)"><strong>UsbKmdfIrql</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbkmdfirql.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql&lt;/strong&gt;](kmdf-usbkmdfirql.md)"> <strong>UsbKmdfIrql</strong> </a>ルールでは、KMDF ドライバーは呼び出さないことに固有の USB デバイス ドライバー インターフェイス (DDI) 不適切な IRQL でレベルを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="kmdf-usbkmdfirql2.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql2&lt;/strong&gt;](kmdf-usbkmdfirql2.md)"><strong>UsbKmdfIrql2</strong></a></p></td>
<td align="left"><p><a href="kmdf-usbkmdfirql2.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrql2&lt;/strong&gt;](kmdf-usbkmdfirql2.md)"> <strong>UsbKmdfIrql2</strong> </a>ルールは、KMDF ドライバー呼び出さないでください USB 固有 Ddi 不適切な IRQL でレベルを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="usbkmdfirqlexplicit.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrqlExplicit&lt;/strong&gt;](usbkmdfirqlexplicit.md)"><strong>UsbKmdfIrqlExplicit</strong></a></p></td>
<td align="left"><p><a href="usbkmdfirqlexplicit.md" data-raw-source="[&lt;strong&gt;UsbKmdfIrqlExplicit&lt;/strong&gt;](usbkmdfirqlexplicit.md)"> <strong>UsbKmdfIrqlExplicit</strong> </a>ルールは、KMDF Ddi が適切な IRQL レベルと呼ばれることを確認します。 このルールは、すべての EvtIoCallback 関数に適用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdfrequestsendsyncatdispatch.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch&lt;/strong&gt;](wdfrequestsendsyncatdispatch.md)"><strong>WdfRequestSendSyncAtDispatch</strong></a></p></td>
<td align="left"><p><a href="wdfrequestsendsyncatdispatch.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch&lt;/strong&gt;](wdfrequestsendsyncatdispatch.md)"> <strong>WdfRequestSendSyncAtDispatch</strong> </a>ルールを確認、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)"> <strong>WdfRequestSend</strong> </a>関数は、適切な IRQL の優先順位で送信されますレベルです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdfrequestsendsyncatdispatch2.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch2&lt;/strong&gt;](wdfrequestsendsyncatdispatch2.md)"><strong>WdfRequestSendSyncAtDispatch2</strong></a></p></td>
<td align="left"><p><a href="wdfrequestsendsyncatdispatch2.md" data-raw-source="[&lt;strong&gt;WdfRequestSendSyncAtDispatch2&lt;/strong&gt;](wdfrequestsendsyncatdispatch2.md)"> <strong>WdfRequestSendSyncAtDispatch2</strong> </a>ルールを確認、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend" data-raw-source="[&lt;strong&gt;WdfRequestSend&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)"> <strong>WdfRequestSend</strong> </a>関数は、適切な IRQL の優先順位で送信されますレベルです。</p></td>
</tr>
</tbody>
</table>

 

**Irql ルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **Irql**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Irql.sdv**で、 **/check**オプション。 以下に例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





