---
title: ファイル システム フィルター ドライバーの初期化
description: ファイル システム フィルター ドライバーの初期化
ms.assetid: 8a487665-0210-49f5-af91-de78de982506
keywords:
- フィルター ドライバーの初期化
- フィルター ドライバー WDK のファイル システムの初期化
- ファイル システム フィルター ドライバー WDK、初期化しています
- DriverEntry WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fdc1ff1582d1cdd3b3b3f8c81f5b35fc21d4b30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380946"
---
# <a name="initializing-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーの初期化


## <span id="ddk_initializing_a_file_system_filter_driver_if"></span><span id="DDK_INITIALIZING_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは、ファイル システム フィルター ドライバーを初期化するためによく似ています、 **DriverEntry**ルーチンのデバイス ドライバーを初期化します。 ドライバーが読み込まれた後、同じコンポーネント、ドライバーを読み込むことも、ドライバー呼び出しを初期化します、ドライバーの**DriverEntry**ルーチン。 ファイル システム フィルター ドライバーをドライバーがロードされるコンポーネントは I/O マネージャー (開始型を持つサービスのフィルター\_ブート\_開始) または (他のスタートアップの種類) のサービス コントロール マネージャー。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) IRQL でシステム スレッド コンテキストで実行されるルーチン = パッシブ\_レベル。 このルーチンは、ページング可能なことができが破棄されるように、INIT セグメントでなければなりません。 ページング可能なドライバーのコードを作成する方法の詳細については、の「解説」を参照してください。 [ **MmLockPagableCodeSection**](https://msdn.microsoft.com/library/windows/hardware/ff554601)します。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは次のように定義されます。

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

このルーチンでは、2 つの入力パラメーターがあります。 まず、 *DriverObject*は、ファイル システム フィルター ドライバーが読み込まれたときに作成されたドライバー オブジェクトです。 次に、 *RegistryPath*ドライバーのレジストリ キーへのパスを含むカウント対象の Unicode 文字列へのポインターです。

[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ファイル システム フィルター ドライバーのルーチンは、次の手順を実行します。

[コントロールのデバイス オブジェクトを作成します。](creating-the-control-device-object.md)

[IRP ディスパッチ ルーチンを登録します。](registering-irp-dispatch-routines.md)

[高速な I/O ディスパッチ ルーチンを登録します。](registering-fast-i-o-dispatch-routines.md)

[FsFilter コールバック ルーチンを登録します。](registering-fsfilter-callback-routines.md)

[他の必要な初期化を実行します。](performing-any-other-needed-initialization.md)

[\[省略可能な\]コールバック ルーチンを登録します。](-optional--registering-callback-routines.md)

[\[省略可能な\]レジストリのパス文字列のコピーを保存しています](-optional--saving-a-copy-of-the-registry-path-string.md)

[状態を返す](returning-status.md)

 

 




