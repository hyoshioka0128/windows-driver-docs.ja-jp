---
title: RequestFormattedValid ルール (kmdf)
description: RequestFormattedValid ルールでは、ドライバーが、WDF を除く、すべての要求を形式を指定します\_要求\_送信\_オプション\_送信\_AND\_に送信する前に、破棄要求I/O ターゲットの場合。
ms.assetid: b7da37ed-3ca5-472e-a915-82674c9efee3
ms.date: 05/21/2018
keywords:
- RequestFormattedValid ルール (kmdf)
topic_type:
- apiref
api_name:
- RequestFormattedValid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2ad7cd9399ac0b530c392441c965b2b7afd918a9
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392896"
---
# <a name="requestformattedvalid-rule-kmdf"></a>RequestFormattedValid ルール (kmdf)


**RequestFormattedValid**ルールでは、ドライバーが、WDF を除く、すべての要求を形式を指定します\_要求\_送信\_オプション\_送信\_AND\_に I/O のターゲットに送信する前に、破棄要求。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>RequestFormattedValid</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**WdfIoTargetFormatRequestForInternalIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)
[**WdfIoTargetFormatRequestForInternalIoctlOthers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers) 
 [**WdfIoTargetFormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforioctl)
[**WdfIoTargetFormatRequestForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforread) 
 [**WdfIoTargetFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforwrite)
[**WdfRequestFormatRequestUsingCurrentType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestformatrequestusingcurrenttype) 
[ **WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)
[**WdfRequestWdmFormatUsingStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestwdmformatusingstacklocation) 
[ **WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)
[**WdfUsbTargetDeviceFormatRequestForCyclePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcycleport) 
 [ **WdfUsbTargetDeviceFormatRequestForString** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforstring) 
 [ **WdfUsbTargetDeviceFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforurb)
[**WdfUsbTargetPipeFormatRequestForAbort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort) 
[ **WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
[**WdfUsbTargetPipeFormatRequestForReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset) 
 [ **WdfUsbTargetPipeFormatRequestForUrb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb) 
 [ **WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)
 

 





