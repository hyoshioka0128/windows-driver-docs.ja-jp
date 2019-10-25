---
title: 高速 I/O ディスパッチ ルーチンの登録
description: 高速 I/O ディスパッチ ルーチンの登録
ms.assetid: e559d3f2-be33-4a35-8931-4716e6082fc9
keywords:
- 高速 i/o ディスパッチルーチンを登録しています
- ディスパッチルーチン WDK ファイルシステム
- 高速 i/o ディスパッチルーチン WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 477898d6dab474207543ce52bb9214e1481b7dc7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841010"
---
# <a name="registering-fast-io-dispatch-routines"></a>高速 I/O ディスパッチ ルーチンの登録


## <span id="ddk_registering_fast_io_dispatch_routines_if"></span><span id="DDK_REGISTERING_FAST_IO_DISPATCH_ROUTINES_IF"></span>


フィルタードライバーの[**Driverobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンの*driverobject*パラメーターは、フィルタードライバーの[**ドライバーオブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)へのポインターを提供します。

ファイルシステムフィルタードライバーの高速 i/o ディスパッチルーチンを登録するには、高速 i/o ディスパッチテーブルを割り当てて初期化し、高速 i/o ディスパッチルーチンのエントリポイントをテーブルに格納して、テーブルのアドレスを Fasystem.servicemodel Odispatch に格納する必要があります。driver オブジェクトのメンバー。

たとえば、仮想的な "MyLegacyFilter" ドライバーでは、次のように、高速 i/o ディスパッチルーチンのエントリポイントを設定できます。

```cpp
RtlZeroMemory(fastIoDispatch, sizeof(FAST_IO_DISPATCH));
fastIoDispatch->SizeOfFastIoDispatch = sizeof(FAST_IO_DISPATCH);
fastIoDispatch->FastIoCheckIfPossible = MyLegacyFilterIoCheckIfPossible;
fastIoDispatch->FastIoRead = MyLegacyFilterIoRead;
fastIoDispatch->FastIoWrite = MyLegacyFilterIoWrite;
fastIoDispatch->FastIoQueryBasicInfo = MyLegacyFilterIoQueryBasicInfo;
fastIoDispatch->FastIoQueryStandardInfo = MyLegacyFilterIoQueryStandardInfo;
fastIoDispatch->FastIoLock = MyLegacyFilterIoLock;
fastIoDispatch->FastIoUnlockSingle = MyLegacyFilterIoUnlockSingle;
fastIoDispatch->FastIoUnlockAll = MyLegacyFilterIoUnlockAll;
fastIoDispatch->FastIoUnlockAllByKey = MyLegacyFilterIoUnlockAllByKey;
fastIoDispatch->FastIoDeviceControl = MyLegacyFilterIoDeviceControl;
fastIoDispatch->FastIoDetachDevice = MyLegacyFilterIoDetachDevice;
fastIoDispatch->FastIoQueryNetworkOpenInfo = MyLegacyFilterIoQueryNetworkOpenInfo;
fastIoDispatch->MdlRead = MyLegacyFilterIoMdlRead;
fastIoDispatch->MdlReadComplete = MyLegacyFilterIoMdlReadComplete;
fastIoDispatch->PrepareMdlWrite = MyLegacyFilterIoPrepareMdlWrite;
fastIoDispatch->MdlWriteComplete = MyLegacyFilterIoMdlWriteComplete;
fastIoDispatch->FastIoReadCompressed = MyLegacyFilterIoReadCompressed;
fastIoDispatch->FastIoWriteCompressed = MyLegacyFilterIoWriteCompressed;
fastIoDispatch->MdlReadCompleteCompressed = MyLegacyFilterIoMdlReadCompleteCompressed;
fastIoDispatch->MdlWriteCompleteCompressed = MyLegacyFilterIoMdlWriteCompleteCompressed;
fastIoDispatch->FastIoQueryOpen = MyLegacyFilterIoQueryOpen;

DriverObject->FastIoDispatch = fastIoDispatch;
```

 

 




