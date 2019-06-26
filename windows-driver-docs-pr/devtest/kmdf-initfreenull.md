---
title: InitFreeNull ルール (kmdf)
description: InitFreeNull ルールを指定する受信 PWDFDEVICE Ddi\_をパラメーターとして INIT、WDFDEVICE に NULL ポインターを使用して呼び出すことができません\_INIT 構造体。
ms.assetid: 99ced415-9af9-4d06-a10f-4c960897ad5f
ms.date: 05/21/2018
keywords:
- InitFreeNull ルール (kmdf)
topic_type:
- apiref
api_name:
- InitFreeNull
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dfa6ceca0a0b0a32cff568b550e7d55a3b43f3ae
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393246"
---
# <a name="initfreenull-rule-kmdf"></a>InitFreeNull ルール (kmdf)


**InitFreeNull**ルールを指定する受信 PWDFDEVICE Ddi\_を使用して、パラメーターとして INIT を呼び出すことはできません、 **NULL**へのポインターを[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。

フレームワークが指定したメソッドの初期化、 [WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体。 ドライバーを呼び出すと[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)機能のデバイス オブジェクト (FDO) または物理デバイス オブジェクト (PDO) を作成する、 **WdfDeviceCreate**メソッドのセット、最初のパラメーター **NULL**成功した場合。

ドライバーでは、デバイス オブジェクトの初期化メソッドを呼び出すときに、エラーが発生したかどうかまたは[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)ドライバーは WdfDeviceInitFree を呼び出す必要があります。 WdfDeviceInitFree する呼び出しの成功後に、ポインターを設定する必要があります、 [WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体を**NULL** (PWDFDEVICE\_INIT =**NULL**).

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>InitFreeNull</strong>ルール。</p>
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

[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)
[**WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)
[**WdfDeviceInitAssignSDDLString** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring) 
 [ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback) 
 [ **WdfDeviceInitFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitfree)
[**WdfDeviceInitRegisterPnpStateChangeCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpnpstatechangecallback) 
 [ **WdfDeviceInitRegisterPowerPolicyStateChangeCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerpolicystatechangecallback)
[**WdfDeviceInitRegisterPowerStateChangeCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitregisterpowerstatechangecallback)
 [ **WdfPdoInitAddCompatibleID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddcompatibleid)
[**WdfPdoInitAddDeviceText** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitadddevicetext) 
[ **WdfPdoInitAddHardwareID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitaddhardwareid)
[**WdfPdoInitAssignDeviceID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigndeviceid)
 [ **WdfPdoInitAssignInstanceID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassigninstanceid)
[**WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)も参照してください
--------

[**InitFreeDeviceCallback**](kmdf-initfreedevicecallback.md)
[**InitFreeDeviceCreate**](kmdf-initfreedevicecreate.md)
[**InitFreeDeviceCreateType2** ](kmdf-initfreedevicecreatetype2.md) 
 [ **PdoInitFreeDeviceCreateType2**](kmdf-pdoinitfreedevicecreatetype2.md)
[**InitFreeDeviceCreateType4** ](kmdf-initfreedevicecreatetype4.md) 
 [ **PdoInitFreeDeviceCallback**](kmdf-pdoinitfreedevicecallback.md)
[**PdoInitFreeDeviceCreate**](kmdf-pdoinitfreedevicecreate.md) 
 [ **PdoInitFreeDeviceCreateType4**](kmdf-pdoinitfreedevicecreatetype4.md)
 

 





