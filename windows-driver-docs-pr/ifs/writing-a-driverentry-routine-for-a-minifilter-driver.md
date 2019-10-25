---
title: ミニフィルタードライバーの DriverEntry ルーチンを記述する
description: ミニフィルタードライバーの DriverEntry ルーチンを記述する
ms.assetid: 949b4087-47de-4145-87dd-d618db44a15b
keywords:
- ファイルシステムミニフィルタードライバー WDK、DriverEntry ルーチン
- ミニフィルタードライバー WDK、DriverEntry ルーチン
- DriverEntry WDK ファイルシステム
- グローバル初期化 WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c385a408093829dcb97fae20da5deb6e81605596
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840928"
---
# <a name="writing-a-driverentry-routine-for-a-minifilter-driver"></a>ミニフィルタードライバーの DriverEntry ルーチンを記述する


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


すべてのファイルシステムミニフィルタードライバーに[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンが必要です。 **Driverentry**ルーチンは、ミニフィルタードライバーが読み込まれるときに呼び出されます。

**Driverentry**ルーチンは、グローバルな初期化を実行し、ミニフィルタードライバーを登録し、フィルター処理を開始します。 このルーチンは、IRQL 受動\_レベルでシステムスレッドコンテキストで実行されます。

**Driverentry**ルーチンは次のように定義されています。

```cpp
NTSTATUS 
(*PDRIVER_INITIALIZE) ( 
    IN PDRIVER_OBJECT DriverObject, 
    IN PUNICODE_STRING RegistryPath 
    ); 
```

**Driverentry**に2つの入力パラメーターがあります。 最初の*Driverobject*は、ミニフィルタードライバーが読み込まれたときに作成されたドライバーオブジェクトです。 2番目の*RegistryPath*は、ミニフィルタードライバーのレジストリキーへのパスを含む、カウントされた Unicode 文字列へのポインターです。

ミニフィルタードライバーの**Driverentry**ルーチンでは、次の手順を順番に実行する必要があります。

1.  ミニフィルタードライバーに必要なグローバル初期化を実行します。

2.  [**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)を呼び出してミニフィルタードライバーを登録します。

3.  [**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)を呼び出してフィルター処理を開始します。

4.  適切な NTSTATUS 値を返します。

このセクションの内容は次のとおりです。

[ミニフィルタードライバーを登録しています](registering-the-minifilter-driver.md)

[フィルター処理の開始](initiating-filtering.md)

[ミニフィルター DriverEntry ルーチンから状態を返す](returning-status.md)

 

 




