---
title: ディスパッチ ルーチンの記述
description: ディスパッチ ルーチンの記述
ms.assetid: 84eb9372-2ef7-4cc2-94af-97e3399e69e0
keywords:
- ディスパッチ ルーチン WDK カーネル
- 標準のドライバーのルーチンの WDK カーネル、ディスパッチ ルーチン
- ドライバーのルーチンの WDK カーネル、ディスパッチ ルーチン
- ルーチンの WDK カーネル、ディスパッチ ルーチン
- システム容量のメモリ割り当ての WDK カーネル
- システム リソースのストレージの WDK カーネル
- システム リソースを格納します。
- ディスパッチ ルーチンは、ディスパッチ ルーチンの WDK カーネル
- Irp WDK カーネルでは、ディスパッチ ルーチン
- 複数の I/O 関数コードの WDK カーネル
- IRP の主な機能コードの WDK カーネル
- 主な機能コードの WDK カーネル
- 関数コードの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09de7bb9b754ab73e264c7a1f0bafff75df7f076
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374114"
---
# <a name="writing-dispatch-routines"></a>ディスパッチ ルーチンの記述





ドライバーを処理するために登録するディスパッチ ルーチンの開始、I/O 要求パケット (IRP) を処理する[IRP の主な機能コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)(<strong>IRP\_MJ\_* XXX</strong><em>).ドライバーの[ </em> *DriverEntry* <em> ](<https://msdn.microsoft.com/library/windows/hardware/ff544113>)ルーチンがディスパッチ ルーチン内でのドライバーのディスパッチ テーブル内のエントリ ポイントをエクスポートします[ </em> *ドライバー\_オブジェクト** ](<https://msdn.microsoft.com/library/windows/hardware/ff544174>)構造体。

ドライバーは、処理する主要な各 I/O 関数コードの別のディスパッチ ルーチンを提供できます。 または、複数の I/O 関数のコードを処理するディスパッチ ルーチンを記述できます。

このセクションでは、次のトピックについて説明します。

[ディスパッチの日常的な機能](dispatch-routine-functionality.md)

[必要なディスパッチ ルーチン](required-dispatch-routines.md)

[省略可能なディスパッチ ルーチン](optional-dispatch-routines.md)

[ディスパッチ ルーチンは、Irql](dispatch-routines-and-irqls.md)

[ドライバーの I/O スタックの場所を確認します。](when-to-check-the-driver-s-i-o-stack-location.md)

[DispatchCreate、DispatchClose、および DispatchCreateClose ルーチン](dispatchcreate--dispatchclose--and-dispatchcreateclose-routines.md)

[DispatchCleanup ルーチン](dispatchcleanup-routines.md)

[DispatchRead、DispatchWrite、および DispatchReadWrite ルーチン](dispatchread--dispatchwrite--and-dispatchreadwrite-routines.md)

[DispatchDeviceControl および DispatchInternalDeviceControl ルーチン](dispatchdevicecontrol-and-dispatchinternaldevicecontrol-routines.md)

[DispatchPnP ルーチン](dispatchpnp-routines.md)

[DispatchPower ルーチン](dispatchpower-routines.md)

[DispatchQueryInformation ルーチン](dispatchqueryinformation-routines.md)

[DispatchSetInformation ルーチン](dispatchsetinformation-routines.md)

[DispatchFlushBuffers ルーチン](dispatchflushbuffers-routines.md)

[DispatchShutdown ルーチン](dispatchshutdown-routines.md)

[DispatchSystemControl ルーチン](dispatchsystemcontrol-routines.md)

 

 




