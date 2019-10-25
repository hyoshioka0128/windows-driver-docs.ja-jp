---
title: デバイス-専用スレッド
description: デバイス-専用スレッド
ms.assetid: 2e11e2c9-aefd-4b7b-8d80-7eb1da9f7cce
keywords:
- スレッドオブジェクト WDK カーネル
- デバイス専用スレッド WDK カーネル
- 実行時の優先度逆転 WDK カーネル
- PsCreateSystemThread
- Kesetbase優先順位スレッド
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8fa5737f018e7e4970597fb9671d88f0d9fe844
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838750"
---
# <a name="device-dedicated-threads"></a>デバイス-専用スレッド





低速のデバイスまたは使用されていないデバイス (フロッピーコントローラーなど) のドライバーは、デバイス専用システムスレッドを作成することによって、多くの "待機中" の問題を解決することができます。 また、ほとんどのファイルシステムドライバーは、システムワーカースレッドを使用し、ワーカースレッドのコールバックルーチンを提供します。

デバイスドライバーが独自のスレッドコンテキストを持っている場合、またはシステムスレッドコンテキストで実行されている場合、デバイス専用スレッドまたは最上位レベルのドライバーのワーカースレッドコールバックルーチンは、[イベントオブジェクト](event-objects.md)などのディスパッチャーオブジェクトの操作を同期できます。[セマフォオブジェクト](semaphore-objects.md)。ドライバーのデバイス拡張機能の共有通信領域にあります。 たとえば、デバイス専用スレッドは、スレッドのデバイスが使用されていない状態で、セマフォの[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)を呼び出すことによって、共有ディスパッチャーオブジェクトを待機できます。 I/o 操作を実行するためにデバイスドライバーが呼び出されるまで (その時点で、セマフォはシグナル状態に設定されます)、待機中のスレッドは CPU 時間を使用しません。

ドライバーは、 [**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)を呼び出してドライバーまたはデバイス専用のスレッドを作成し、 [**Kesetbase thread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kesetbaseprioritythread)を呼び出してスレッドの基本優先順位を設定できます。 ドライバーでは、SMP コンピューターでの*実行時優先順位の逆転*を回避する優先順位値を指定する必要があります。 つまり、ドライバーによって作成されたスレッドの基本優先順位を設定しすぎると、そのドライバーに i/o 要求を送信する優先順位の低いスレッドの実行に遅延が生じる可能性があります。

スレッドオブジェクト自体はディスパッチャーオブジェクトの一種であるため、スレッドは別のスレッドが完了するまで待機できます。 スレッドに関連付けられているスレッドオブジェクトポインターを取得するために、ドライバーは、 **PsCreateSystemThread**から受信したスレッドハンドルを渡して、 [**Obreferenceobjectbyhandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)を呼び出すことができます。

スレッドは[**Kedelayexecutionthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)を呼び出して、完全なタイムスライスである可能性がある間隔を待機できます。 **Kedelayexecutionthread** interval の粒度は約10ミリ秒です。 **Kedelayexecutionthread**はタイマー駆動型のルーチンであるため、プラットフォームによっては、その間隔の粒度は10ミリ秒よりもわずかに高速または低速になります。

 

 




