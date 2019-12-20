---
title: フレームワーク ファイル オブジェクト
description: フレームワーク ファイル オブジェクト
ms.assetid: dd8215ee-2c10-4e49-9d7f-d2295bf219da
keywords:
- UMDF オブジェクト WDK、ファイルオブジェクト
- フレームワークオブジェクト WDK UMDF、ファイルオブジェクト
- ファイルオブジェクト WDK UMDF
- IWDFFile
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 254d85ff50115524ace7e6baf3979a362e05a283
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210910"
---
# <a name="framework-file-object"></a>フレームワーク ファイル オブジェクト


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

フレームワークファイルオブジェクトは、 [Iwdffile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)インターフェイスによってドライバーに公開されます。 これは、開いているデバイスのフレームワーク表現です。 アプリケーションが Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)関数を使用してデバイスを開くと、開いているデバイスインスタンスを表すファイルオブジェクトがフレームワークによって作成されます。 したがって、フレームワークファイルオブジェクトは、アプリケーションの**CreateFile**への呼び出しから返される Win32 ハンドルと概念的には同じです。 フレームワークでは、1つのデバイスに関連付けられた複数のファイルオブジェクトを作成できます。 各ファイルオブジェクトは、 **CreateFile**の呼び出しが成功するたびに作成されます。 読み取りや書き込みなどのすべての i/o 操作は、特定のファイルオブジェクトインスタンスを対象としています。

UMDF ドライバーに渡されたすべての要求は、ファイルオブジェクトに関連付けられ**て   ます**。 ただし、 [WDM](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)および[kmdf](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)ドライバーに渡された要求は、ファイルオブジェクトに関連付けられていないことがあります。

 

UMDF ドライバーは、 [**IWDFIoRequest:: GetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject)メソッドを呼び出して、要求に関連付けられているファイルオブジェクトを取得できます。

ドライバーが[**Getfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getfileobject)を呼び出すと、フレームワークによってインターフェイスの参照カウントがインクリメントされます。 インターフェイスポインターを使用して終了した場合、ドライバーは参照を解放する必要があります。 これを行うには、オブジェクトがコンテキストの外に出たときに参照カウントを自動的にデクリメントするスマートポインターを使用するか、またはインターフェイスを使用して終了したときに、インターフェイスで[**Release**](https://docs.microsoft.com/windows/desktop/api/unknwn/nf-unknwn-iunknown-release)を呼び出します。 スマートポインターの使用方法を示すコード例については、「 **Getfileobject**」を参照してください。

 

 





