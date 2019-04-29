---
title: Sdv-map.h ファイルの形式
description: Sdv-map.h ファイルの形式
ms.assetid: 1b9e2b8d-04b8-4288-9d63-e7d84d75a9c6
keywords:
- Sdv map.h WDK Static Driver Verifier の形式
- WDK Static Driver Verifier の形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3bc99f130f1cddf240003f6b26234ba732fa39
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329685"
---
# <a name="format-of-the-sdv-maph-file"></a>Sdv-map.h ファイルの形式


Sdv map.h ファイルには、すべてのドライバーおよび関連付けられているコールバック関数とドライバーのエントリ ポイントで宣言されている関数の役割の種類が一覧表示します。

失敗、KMDF サンプル ドライバーの承認済みの Sdv map.h ファイルを次に示します\_Driver3 します。

```
//Approved=true
#define fun_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd
#define fun_WDF_IO_QUEUE_IO_READ EvtIoRead
#define fun_WDF_IO_QUEUE_IO_STOP EvtIoStop
#define fun_WDF_TIMER_1 EvtTimerFunc
#define fun_WDF_DRIVER_UNLOAD EvtDriverUnload
#define fun_WDF_REQUEST_CANCEL_1 EvtRequestCancel
#define fun_DriverEntry DriverEntry
#define fun_WDF_DEVICE_D0_ENTRY DeviceD0Entry
#define fun_WDF_IO_QUEUE_IO_WRITE EvtIoWrite
#define fun_WDF_IO_QUEUE_IO_DEVICE_CONTROL EvtIoDeviceControl
```

SDV には、エントリ ポイントが検出されると、作成、 **\#定義**ディレクティブで、次の形式。

```
#define fun_Function_RoleType EntryPoint
```

 

 





