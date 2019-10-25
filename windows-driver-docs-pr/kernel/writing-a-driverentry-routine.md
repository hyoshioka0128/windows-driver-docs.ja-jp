---
title: DriverEntry ルーチンを記述する
description: DriverEntry ルーチンを記述する
ms.assetid: c33bc82b-6181-4e31-b272-aaadb2d9b058
keywords:
- 標準ドライバールーチン WDK カーネル、DriverEntry ルーチン
- ドライバールーチン WDK カーネル、DriverEntry ルーチン
- ルーチン WDK カーネル、DriverEntry ルーチン
- DriverEntry WDK カーネル
- DriverEntry WDK カーネル、DriverEntry ルーチンについて
- ドライバーの初期化 WDK カーネル
- ドライバーの初期化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 965ba1329242a88fa6ce67a027d936bc6019c916
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835623"
---
# <a name="writing-a-driverentry-routine"></a>DriverEntry ルーチンを記述する





各ドライバーには、ドライバー全体のデータ構造とリソースを初期化する[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンが必要です。 I/o マネージャーは、ドライバーの読み込み時に**Driverentry**ルーチンを呼び出します。

プラグアンドプレイ (PnP) をサポートするドライバーでは、すべてのドライバーが必要とするため、 **Driverentry**ルーチンは*ドライバー*の初期化を行い、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチン (および場合によっては、pnp IRP を処理するディスパッチルーチン[ **\_の\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)の要求の開始) は、*デバイス*の初期化を担当します。 ドライバーの初期化には、ドライバーのその他のエントリポイントのエクスポート、ドライバーが使用する特定のオブジェクトの初期化、ドライバーごとのシステムリソースの設定などが含まれます。 (PnP 以外のドライバーについては、「Driver Development Kit \[DDK\] for Microsoft Windows NT 4.0 以前」で説明されているように、大幅に異なる要件があります)。

**Driverentry**ルーチンは、IRQL = パッシブ\_レベルでシステムスレッドのコンテキストで呼び出されます。

**Driverentry**ルーチンは、ページングが可能であり、破棄されるように INIT セグメントに含まれている必要があります。 Windows Driver Kit (WDK) に付属しているサンプルドライバーに示されているように、 **alloc\_text** pragma ディレクティブを使用します。

このセクションは、次のトピックで構成されています。

[DriverEntry の必要な責任](driverentry-s-required-responsibilities.md)

[DriverEntry のオプションの役割](driverentry-s-optional-responsibilities.md)

[DriverEntry の戻り値](driverentry-return-values.md)

 

 




