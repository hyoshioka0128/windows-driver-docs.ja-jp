---
title: ミニフィルター ドライバー用の DriverEntry ルーチンの記述
description: ミニフィルター ドライバー用の DriverEntry ルーチンの記述
ms.assetid: 949b4087-47de-4145-87dd-d618db44a15b
keywords:
- ファイル システム ミニフィルター ドライバー WDK、DriverEntry ルーチン
- ミニフィルター ドライバー WDK、DriverEntry ルーチン
- DriverEntry WDK ファイル システム
- グローバル初期化 WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4730883cc7668e781af09d90a675e62d6c37744e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371286"
---
# <a name="writing-a-driverentry-routine-for-a-minifilter-driver"></a>ミニフィルター ドライバー用の DriverEntry ルーチンの記述


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


ファイル システム ミニフィルター ドライバーが必要、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 **DriverEntry**ミニフィルター ドライバーが読み込まれるときに、ルーチンが呼び出されます。

**DriverEntry**ルーチンは、グローバル初期化を実行します、ミニフィルター ドライバーを登録し、フィルター処理を開始します。 このルーチンは IRQL パッシブにシステム スレッド コンテキストで実行される\_レベル。

**DriverEntry**ルーチンは次のように定義されます。

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

**DriverEntry**が 2 つの入力パラメーター。 まず、 *DriverObject*、ミニフィルター ドライバーが読み込まれたときに作成されたドライバー オブジェクトです。 次に、 *RegistryPath*、ミニフィルター ドライバーのレジストリ キーへのパスを含むカウント対象の Unicode 文字列へのポインターです。

ミニフィルター ドライバーの**DriverEntry**ルーチンの順序で、次の手順を実行する必要があります。

1.  ミニフィルター ドライバー、必要なグローバル初期化を実行します。

2.  ミニフィルター ドライバーを呼び出すことによって登録[ **FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)します。

3.  呼び出すことによってフィルター処理を開始[ **FltStartFiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltstartfiltering)します。

4.  適切な NTSTATUS 値を返します。

このセクションの内容:

[ミニフィルター ドライバーの登録](registering-the-minifilter-driver.md)

[フィルター処理を開始します。](initiating-filtering.md)

[ミニフィルター DriverEntry ルーチンから状態を返す](returning-status.md)

 

 




