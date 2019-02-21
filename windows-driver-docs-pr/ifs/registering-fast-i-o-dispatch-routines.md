---
title: 高速な I/O ディスパッチ ルーチンを登録します。
description: 高速な I/O ディスパッチ ルーチンを登録します。
ms.assetid: e559d3f2-be33-4a35-8931-4716e6082fc9
keywords:
- 高速の I/O ディスパッチ ルーチンを登録します。
- ディスパッチ ルーチン WDK ファイル システム
- 高速な I/O ディスパッチ ルーチン WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07967e2347cd4a7f41edfa80e80ee196969d8850
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537790"
---
# <a name="registering-fast-io-dispatch-routines"></a>高速な I/O ディスパッチ ルーチンを登録します。


## <span id="ddk_registering_fast_io_dispatch_routines_if"></span><span id="DDK_REGISTERING_FAST_IO_DISPATCH_ROUTINES_IF"></span>


*DriverObject*パラメーター、フィルター ドライバーの[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは、フィルター ドライバーへのポインターを提供[**ドライバーオブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)します。

ファイル システム フィルター ドライバーの高速な I/O ディスパッチ ルーチンを登録する必要がありますを割り当てると高速な I/O ディスパッチ テーブルを初期化、テーブルに高速の I/O ディスパッチ ルーチンのエントリ ポイントを格納および内のテーブルのアドレスを格納、 **FastIoDispatch**ドライバー オブジェクトのメンバー。

たとえば、仮想的な"MyLegacyFilter"ドライバーは次の手順の高速の I/O ディスパッチ ルーチンのエントリ ポイントを設定できます。

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

 

 




