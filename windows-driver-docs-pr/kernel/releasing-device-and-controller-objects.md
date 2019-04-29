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
ms.openlocfilehash: c12a6540d93822d262f4b687ffdd8de0214fa4e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324472"
---
# <a name="releasing-device-and-controller-objects"></a>デバイス オブジェクトとコントローラー オブジェクトの解放





ドライバーがデバイスまたはコント ローラーのオブジェクトを削除する前に、やコント ローラー拡張機能、対応するデバイスに保存しておいた割り込みオブジェクトに他のドライバーのオブジェクトへのポインターなどの外部リソースへの参照を解放する必要があります。 呼び出して[ **IoDeleteDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549083)ドライバーを作成する各デバイス オブジェクト。 以前に呼び出されている非 WDM ドライバー [ **IoCreateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548395)も呼び出す必要があります[ **IoDeleteController**](https://msdn.microsoft.com/library/windows/hardware/ff549078)します。

ドライバーがデバイスの拡張機能での記憶域を提供する任意のカーネル定義オブジェクトが自動的に解放されるときに、 [*アンロード*](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンの呼び出し**IoDeleteDevice**で対応するデバイス オブジェクト。 一般に、いずれかのオブジェクト、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)または[*を再初期化*](https://msdn.microsoft.com/library/windows/hardware/ff561022)ルーチンを呼び出すことによってセットアップ**KeInitialize *Xxx*** への呼び出しによって解放できる**IoDeleteDevice**場合は、ドライバーは、そのデバイスの拡張機能では、そのオブジェクトのストレージを提供します。 たとえば、ドライバーがある、 [ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンがそのデバイスの拡張への呼び出しで必要な DPC とタイマー オブジェクトのストレージを提供された**IoDeleteDevice**これらのシステム リソースを解放します。

同様に、ドライバーが記憶域コント ローラーの拡張機能を提供する任意のカーネル定義オブジェクトは、自動的に解放されるときに、*アンロード*ルーチンの呼び出し**IoDeleteController**で、コント ローラーの対応するオブジェクト。

場合、 **DriverEntry**または*を再初期化*というルーチン[ **IoGetConfigurationInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549157)のカウントをインクリメントする、特定の種類のデバイス、*アンロード*ルーチンも呼び出す必要があります**IoGetConfigurationInformation** I/O マネージャーのグローバル構成では、デバイスのカウントをデクリメントし、ほど情報構造体は、デバイスの対応するオブジェクトを削除します。

制御を返す前に、*アンロード*ルーチンもはその他のドライバーに割り当てられたリソースその他のドライバーのルーチンで解放されていないを解放する責任を負います。

 

 




