---
title: 一般 I/O ターゲットに関する情報の取得
description: 一般 I/O ターゲットに関する情報の取得
ms.assetid: 70ae920e-de2d-4014-bae4-74058b26e7c0
keywords:
- 一般的な i/o ターゲット WDK KMDF、情報
- 状態情報 WDK KMDF、一般的な i/o ターゲット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 743f41e1aa339d767408ff41ec95b58e070038b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843139"
---
# <a name="obtaining-information-about-a-general-io-target"></a>一般 I/O ターゲットに関する情報の取得


I/o ターゲットに関する情報を取得するために、ドライバーは、i/o ターゲットオブジェクトによって定義される次のメソッドを呼び出すことができます。

<a href="" id="---------wdfiotargetgetdevice--------"></a>[**WdfIoTargetGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetdevice)  
ローカルまたはリモートの i/o ターゲットに関連付けられているフレームワークデバイスオブジェクトを返します。

<a href="" id="wdfiotargetquerytargetproperty-or-wdfiotargetallocandquerytargetproperty"></a>[**WdfIoTargetQueryTargetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetquerytargetproperty)または[ **WdfIoTargetAllocAndQueryTargetProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetallocandquerytargetproperty)  
ローカルまたはリモートの i/o ターゲットデバイスに関連付けられているデバイスプロパティを取得します。

<a href="" id="---------wdfiotargetgetstate--------"></a>[**WdfIoTargetGetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetgetstate)  
ローカルまたはリモートの i/o ターゲットの状態情報を返します。

<a href="" id="---------wdfiotargetwdmgettargetdeviceobject--------"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetdeviceobject)  
ローカルまたはリモートの i/o ターゲットに関連付けられている Windows Driver Model (WDM) デバイスオブジェクトへのポインターを返します。

<a href="" id="---------wdfiotargetwdmgettargetphysicaldevice--------"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetphysicaldevice)  
リモート i/o ターゲットのデバイスを表す WDM 物理デバイスオブジェクト (PDO) へのポインターを返します。

<a href="" id="---------wdfiotargetwdmgettargetfileobject--------"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfileobject)  
リモート i/o ターゲットに関連付けられている WDM ファイルオブジェクトへのポインターを返します。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetwdmgettargetfilehandle)  
リモート i/o ターゲットに関連付けられているファイルへのハンドルを返します。

 

 





