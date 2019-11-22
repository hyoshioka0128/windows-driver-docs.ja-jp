---
title: DispatchCreate、DispatchClose、DispatchCreateClose ルーチン
description: DispatchCreate、DispatchClose、DispatchCreateClose ルーチン
ms.assetid: 5c1c0036-71b1-4410-b157-f9ebe3b6ecfc
keywords:
- ディスパッチルーチン WDK カーネル、DispatchCreate ルーチン
- ディスパッチルーチン WDK カーネル、DispatchClose ルーチン
- ディスパッチルーチン WDK カーネル、DispatchCreateClose ルーチン
- DispatchCreateClose ルーチン
- DispatchClose ルーチン
- DispatchCreate ルーチン
- IRP_MJ_CREATE i/o 関数コード
- IRP_MJ_CLOSE i/o 関数コード
- ディスパッチルーチン WDK カーネルを作成する
- ディスパッチルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8ba65849767383f5b4d0f66a4e0cb715a71c86
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838733"
---
# <a name="dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose、DispatchCreateClose ルーチン





[**Irp\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create) 、および[**irp\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)の i/o 関数コードを含むドライバーの[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) irp。 また、結合された[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、これらの i/o 関数コードの両方に対して irp を処理できます。

作成要求は、デバイス (アプリケーションまたはサブシステムレベルのドライバーに代わって) を表すファイルオブジェクトへのハンドルをユーザーモードサブシステムが取得しようとするか、またはより高いレベルのドライバーの[**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)または[**ioattachdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevice)への呼び出しで発生することがあります。

逆方向の要求は、ドライバーのデバイスオブジェクトに関連付けられているファイルオブジェクトハンドルのユーザーモードサブシステムの close に由来します。

これらの要求はそれぞれ、本質的に同期されています。

 

 




