---
title: ファイル システム フィルター ドライバーの初期化
description: ファイル システム フィルター ドライバーの初期化
ms.assetid: 8a487665-0210-49f5-af91-de78de982506
keywords:
- フィルタードライバーの初期化
- フィルタードライバー WDK ファイルシステム、初期化
- ファイルシステムフィルタードライバー WDK, 初期化
- DriverEntry WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49f2a025fd1d6ce3aaf79cbc72bb346bc3473ef6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841200"
---
# <a name="initializing-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーの初期化


## <span id="ddk_initializing_a_file_system_filter_driver_if"></span><span id="DDK_INITIALIZING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


ファイルシステムフィルタードライバーを初期化する[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、デバイスドライバーを初期化するための**driverentry**ルーチンとよく似ています。 ドライバーが読み込まれた後、ドライバーを読み込んだ同じコンポーネントも、ドライバーの**Driverentry**ルーチンを呼び出すことによってドライバーを初期化します。 ファイルシステムフィルタードライバーの場合、ドライバーを読み込むコンポーネントは、i/o マネージャー (start type が SERVICE\_BOOT\_START) またはサービスコントロールマネージャー (他の開始の種類の場合) のいずれかです。

[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、IRQL = パッシブ\_レベルでシステムスレッドコンテキストで実行されます。 このルーチンは、ページングが可能であり、破棄されるように INIT セグメントに存在する必要があります。 ドライバーコードをページング可能にする方法の詳細については、 [**MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection)の「解説」を参照してください。

[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは次のように定義されています。

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

このルーチンには2つの入力パラメーターがあります。 最初の*Driverobject*は、ファイルシステムフィルタードライバーが読み込まれたときに作成されたドライバーオブジェクトです。 2番目の*RegistryPath*は、ドライバーのレジストリキーへのパスを含む、カウントされた Unicode 文字列へのポインターです。

ファイルシステムフィルタードライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、次の手順を実行します。

[コントロールデバイスオブジェクトの作成](creating-the-control-device-object.md)

[IRP ディスパッチルーチンを登録しています](registering-irp-dispatch-routines.md)

[高速 i/o ディスパッチルーチンを登録しています](registering-fast-i-o-dispatch-routines.md)

[FsFilter コールバックルーチンを登録しています](registering-fsfilter-callback-routines.md)

[その他の必要な初期化を実行しています](performing-any-other-needed-initialization.md)

[\[オプション\] コールバックルーチンの登録](-optional--registering-callback-routines.md)

[\[オプション\] レジストリパス文字列のコピーを保存します。](-optional--saving-a-copy-of-the-registry-path-string.md)

[ステータスを返す](returning-status.md)

 

 




