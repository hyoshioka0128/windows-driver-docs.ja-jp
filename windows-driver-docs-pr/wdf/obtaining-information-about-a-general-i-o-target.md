---
title: 一般 I/O ターゲットに関する情報の取得
description: 一般 I/O ターゲットに関する情報の取得
ms.assetid: 70ae920e-de2d-4014-bae4-74058b26e7c0
keywords:
- 一般的な I/O に関する WDK KMDF、情報をターゲットします。
- WDK KMDF、一般的な I/O ターゲットの状態情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 315fbd836e62c383767ef1bf7717c949e3daf96c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376670"
---
# <a name="obtaining-information-about-a-general-io-target"></a>一般 I/O ターゲットに関する情報の取得


I/O ターゲットに関する情報を取得するには、ドライバーは、I/O のターゲット オブジェクトを定義する次のメソッドを呼び出すことができます。

<a href="" id="---------wdfiotargetgetdevice--------"></a>[**WdfIoTargetGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetgetdevice)  
ローカルまたはリモートの I/O ターゲットに関連付けられている framework デバイス オブジェクトを返します。

<a href="" id="wdfiotargetquerytargetproperty-or-wdfiotargetallocandquerytargetproperty"></a>[**WdfIoTargetQueryTargetProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetquerytargetproperty)または[ **WdfIoTargetAllocAndQueryTargetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetallocandquerytargetproperty)  
ローカルまたはリモート I/O ターゲットのデバイスに関連付けられているデバイスのプロパティを取得します。

<a href="" id="---------wdfiotargetgetstate--------"></a>[**WdfIoTargetGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate)  
状態のローカルまたはリモートの I/O ターゲットの情報を返します。

<a href="" id="---------wdfiotargetwdmgettargetdeviceobject--------"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
ローカルまたはリモートの I/O ターゲットに関連付けられている Windows Driver Model (WDM) デバイス オブジェクトへのポインターを返します。

<a href="" id="---------wdfiotargetwdmgettargetphysicaldevice--------"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
リモートの I/O ターゲット デバイスを表す WDM 物理デバイス オブジェクト (PDO) へのポインターを返します。

<a href="" id="---------wdfiotargetwdmgettargetfileobject--------"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
リモートの I/O ターゲットに関連付けられている WDM ファイル オブジェクトへのポインターを返します。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
リモートの I/O ターゲットに関連付けられているファイル ハンドルを返します。

 

 





