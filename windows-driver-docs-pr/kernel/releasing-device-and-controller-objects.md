---
title: デバイス オブジェクトとコントローラー オブジェクトの解放
description: デバイス オブジェクトとコントローラー オブジェクトの解放
ms.assetid: 35404401-d3a8-4257-b1a3-b16ebe42b181
keywords:
- ルーチン WDK カーネルでは、非 PnP ドライバーをアンロードします。
- WDK カーネルの日常的な非 PnP アンロード
- デバイスをリリース
- コント ローラーのオブジェクトを解放します。
- デバイスは、WDK のカーネルを解放します。
- コント ローラー オブジェクトの WDK カーネルの解放
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 179975775388ccc51c8f340e74c4f52df0ff9ce6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373441"
---
# <a name="releasing-device-and-controller-objects"></a>デバイス オブジェクトとコントローラー オブジェクトの解放





ドライバーがデバイスまたはコント ローラーのオブジェクトを削除する前に、やコント ローラー拡張機能、対応するデバイスに保存しておいた割り込みオブジェクトに他のドライバーのオブジェクトへのポインターなどの外部リソースへの参照を解放する必要があります。 呼び出して[ **IoDeleteDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)ドライバーを作成する各デバイス オブジェクト。 以前に呼び出されている非 WDM ドライバー [ **IoCreateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatecontroller)も呼び出す必要があります[ **IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iodeletecontroller)します。

ドライバーがデバイスの拡張機能での記憶域を提供する任意のカーネル定義オブジェクトが自動的に解放されるときに、 [*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンの呼び出し**IoDeleteDevice**で対応するデバイス オブジェクト。 一般に、いずれかのオブジェクト、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)または[*を再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)ルーチンを呼び出すことによってセットアップ**KeInitialize *Xxx*** への呼び出しによって解放できる**IoDeleteDevice**場合は、ドライバーは、そのデバイスの拡張機能では、そのオブジェクトのストレージを提供します。 たとえば、ドライバーがある、 [ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンがそのデバイスの拡張への呼び出しで必要な DPC とタイマー オブジェクトのストレージを提供された**IoDeleteDevice**これらのシステム リソースを解放します。

同様に、ドライバーが記憶域コント ローラーの拡張機能を提供する任意のカーネル定義オブジェクトは、自動的に解放されるときに、*アンロード*ルーチンの呼び出し**IoDeleteController**で、コント ローラーの対応するオブジェクト。

場合、 **DriverEntry**または*を再初期化*というルーチン[ **IoGetConfigurationInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iogetconfigurationinformation)のカウントをインクリメントする、特定の種類のデバイス、*アンロード*ルーチンも呼び出す必要があります**IoGetConfigurationInformation** I/O マネージャーのグローバル構成では、デバイスのカウントをデクリメントし、ほど情報構造体は、デバイスの対応するオブジェクトを削除します。

制御を返す前に、*アンロード*ルーチンもはその他のドライバーに割り当てられたリソースその他のドライバーのルーチンで解放されていないを解放する責任を負います。

 

 




