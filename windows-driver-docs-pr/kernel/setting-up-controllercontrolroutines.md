---
title: ControllerControl ルーチンのセットアップ
description: ControllerControl ルーチンのセットアップ
ms.assetid: 007247c1-b51e-4677-9a46-78ff9f1c8996
keywords:
- コントローラーオブジェクト WDK カーネル、コントローラー制御ルーチンの記述
- コントローラー制御ルーチン、書き込み
- コントローラーコントロールルーチン、設定
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: da0624a283feb036ff4d789f53ba5fa1bf456647
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836355"
---
# <a name="setting-up-controllercontrol-routines"></a>ControllerControl ルーチンのセットアップ





ドライバーの[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、\_デバイス要求を開始して、[*コントローラー制御*](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチンを設定するために、 [**IRP\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)を受け取ったときに、次の操作を行う必要があります。

1.  [**IoCreateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatecontroller)を呼び出して、コントローラーオブジェクトを設定します。これは、システムが非ページプールから割り当て、ゼロで初期化するコントローラー拡張機能の*サイズ*を指定します。

2.  **IoCreateController**によって返されるコントローラー*オブジェクトポインターを保存します*。通常は、コントローラーオブジェクトによって表されるハードウェアによって制御される物理デバイスまたは論理デバイスを表す各デバイスオブジェクトのデバイス拡張機能に格納します。

3.  ドライバーによって決定された * コントローラーの内容を設定または初期化します * **-&gt;コントローラー拡張機能**です。

返されるのは、返された*コントローラーのオブジェクト*ポインター、ドライバーの DeviceObject*制御*ルーチンのエントリポイント、現在の IRP のターゲットデバイスを表すポインター、および既に設定されている領域への*コンテキスト*ポインターです。ドライバーの[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)への呼び出しで、*コントローラー*の呼び出しを行う必要があります。 通常、ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンは、 **IoAllocateController**を呼び出す前に、*コンテキスト*で領域を設定します。

 

 




