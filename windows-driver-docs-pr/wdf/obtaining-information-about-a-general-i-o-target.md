---
title: 一般 I/O ターゲットに関する情報の取得
description: 一般 I/O ターゲットに関する情報の取得
ms.assetid: 70ae920e-de2d-4014-bae4-74058b26e7c0
keywords:
- 一般的な I/O に関する WDK KMDF、情報をターゲットします。
- WDK KMDF、一般的な I/O ターゲットの状態情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf5d87c4e59010fd69377ca112233415028d816f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390129"
---
# <a name="obtaining-information-about-a-general-io-target"></a>一般 I/O ターゲットに関する情報の取得


I/O ターゲットに関する情報を取得するには、ドライバーは、I/O のターゲット オブジェクトを定義する次のメソッドを呼び出すことができます。

<a href="" id="---------wdfiotargetgetdevice--------"></a>[**WdfIoTargetGetDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548625)  
ローカルまたはリモートの I/O ターゲットに関連付けられている framework デバイス オブジェクトを返します。

<a href="" id="wdfiotargetquerytargetproperty-or-wdfiotargetallocandquerytargetproperty"></a>[**WdfIoTargetQueryTargetProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff548646)または[ **WdfIoTargetAllocAndQueryTargetProperty**](https://msdn.microsoft.com/library/windows/hardware/ff548585)  
ローカルまたはリモート I/O ターゲットのデバイスに関連付けられているデバイスのプロパティを取得します。

<a href="" id="---------wdfiotargetgetstate--------"></a>[**WdfIoTargetGetState**](https://msdn.microsoft.com/library/windows/hardware/ff548631)  
状態のローカルまたはリモートの I/O ターゲットの情報を返します。

<a href="" id="---------wdfiotargetwdmgettargetdeviceobject--------"></a>[**WdfIoTargetWdmGetTargetDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff548682)  
ローカルまたはリモートの I/O ターゲットに関連付けられている Windows Driver Model (WDM) デバイス オブジェクトへのポインターを返します。

<a href="" id="---------wdfiotargetwdmgettargetphysicaldevice--------"></a>[**WdfIoTargetWdmGetTargetPhysicalDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548691)  
リモートの I/O ターゲット デバイスを表す WDM 物理デバイス オブジェクト (PDO) へのポインターを返します。

<a href="" id="---------wdfiotargetwdmgettargetfileobject--------"></a>[**WdfIoTargetWdmGetTargetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548686)  
リモートの I/O ターゲットに関連付けられている WDM ファイル オブジェクトへのポインターを返します。

<a href="" id="wdfiotargetwdmgettargetfilehandle"></a>[**WdfIoTargetWdmGetTargetFileHandle**](https://msdn.microsoft.com/library/windows/hardware/ff548683)  
リモートの I/O ターゲットに関連付けられているファイル ハンドルを返します。

 

 





