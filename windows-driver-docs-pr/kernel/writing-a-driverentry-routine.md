---
title: DriverEntry ルーチンの記述
description: DriverEntry ルーチンの記述
ms.assetid: c33bc82b-6181-4e31-b272-aaadb2d9b058
keywords:
- 標準のドライバーのルーチンの WDK カーネル、DriverEntry ルーチン
- ドライバーのルーチンの WDK カーネル、DriverEntry ルーチン
- driverentry ルーチン WDK カーネル
- DriverEntry WDK カーネル
- DriverEntry ルーチンについての DriverEntry WDK カーネル
- ドライバーの初期化の WDK カーネル
- ドライバーの初期化
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc16d18213a3f73e2c265040bdca372cca294e35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374150"
---
# <a name="writing-a-driverentry-routine"></a>DriverEntry ルーチンの記述





各ドライバーが必要、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンで、ドライバー レベルのデータ構造とリソースを初期化します。 I/O マネージャーの呼び出し、 **DriverEntry**ルーチン、ドライバーの読み込み時にします。

すべてのドライバーが、プラグ アンド プレイ (PnP) をサポートするドライバー、 **DriverEntry**ルーチンは責任を負います*ドライバー*の初期化中に、 [ *AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン (し、PnP を処理するディスパッチ ルーチンではおそらく、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求) は、責任を負います*デバイス*初期化します。 ドライバーの初期化には、ドライバーの初期化中、他のエントリ ポイントのエクスポートが含まれています。 特定のオブジェクト、ドライバーの使用、およびさまざまなドライバーごとのシステム リソースを設定します。 (ドライバー開発キットの説明に従って、非 PnP ドライバーが大幅に用途を持つ\[DDK\] for Microsoft Windows NT 4.0 以降です)。

**DriverEntry**ルーチンは IRQL でシステムのスレッドのコンテキストで呼び出される = パッシブ\_レベル。

A **DriverEntry**ルーチンがページング可能なことができ、INIT セグメントは破棄されるようにする必要があります。 使用して、**アロケーション\_テキスト**プラグマ ディレクティブは、Windows Driver Kit (WDK) で提供されるサンプル ドライバーに示すようにします。

このセクションでは、次のトピックについて説明します。

[DriverEntry の必要な責任](driverentry-s-required-responsibilities.md)

[DriverEntry の省略可能な責任](driverentry-s-optional-responsibilities.md)

[DriverEntry 戻り値します。](driverentry-return-values.md)

 

 




