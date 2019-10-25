---
title: ISR の登録
description: ISR の登録
ms.assetid: 903e5664-2193-4456-b133-bb979d700bdf
keywords:
- 割り込みサービスルーチンの WDK カーネル、Isr の登録
- 割り込みオブジェクト WDK カーネル、Isr の登録
- Isr WDK カーネル, Isr の登録
- Isr WDK カーネルを登録しています
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1e3b1239dad90aaf9ca1cf570de07a6eedb2702
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827569"
---
# <a name="registering-an-isr"></a>ISR の登録


ドライバーは、 [**IoConnectInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterruptex)ルーチンを使用して、割り込みの ISR を登録します。 **IoConnectInterruptEx**は、Windows Vista 以降のオペレーティングシステムの一部です。 **IoConnectInterruptEx**は1つの*パラメーター*パラメーターを受け取ります。これは、 [**IO\_接続\_INTERRUPT\_Parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_connect_interrupt_parameters)構造体へのポインターです。 Windows Server 2003、Windows XP、および Windows 2000 では、ドライバーは Windows Driver Kit (WDK) に含まれている Iointex .lib ライブラリを使用できます。

Windows Vista 以降では、 **IoConnectInterruptEx**は、ISR を登録するためのいくつかの異なる方法を提供します。 次のように、&gt;**バージョン**-*パラメーター*に指定された値によってメソッドが決まります。

-   デバイスのすべての行ベースの割り込みに[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンを登録するには、CONNECT\_LINE\_ベースを使用します。 (デバイスの場合、通常は最大で1行の割り込みが必要です)。システムは、デバイスに割り当てられた行ベースの割り込みを自動的に検出します。 詳細については、「 [Using THE CONNECT\_LINE\_BASED Version Of IoConnectInterruptEx](using-the-connect-line-based-version-of-ioconnectinterruptex.md)」を参照してください。

-   デバイスのメッセージシグナルによる割り込みのすべてに[*InterruptMessageService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kmessage_service_routine)ルーチンを登録するには、CONNECT\_message\_を使用します。 フォールバック[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンを指定することもできます。デバイスに行ベースの割り込みがある場合、 **IoConnectInterruptEx**は*InterruptService*ルーチンを代わりに登録します。 システムは、デバイスに割り当てられたメッセージシグナル割り込みを自動的に検出します。 詳細については、「 [Using THE CONNECT\_MESSAGE\_BASED Version Of IoConnectInterruptEx](using-the-connect-message-based-version-of-ioconnectinterruptex.md)」を参照してください。

-   各割り込みの*InterruptService*ルーチンを個別に登録するには、CONNECT\_完全\_を使用します。 これを使用すると、行ベースまたはメッセージシグナルの割り込みに*InterruptService*ルーチンを指定できますが、PnP マネージャーによって渡された情報を使用して割り込みを手動で指定する必要があります。 詳細については、「 [Using THE CONNECT\_\_指定されたバージョンの IoConnectInterruptEx を完全に使用する](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)」を参照してください。

Windows Vista より前のオペレーティングシステムでは、指定された完全\_接続\_のみ使用できます。 CONNECT\_LINE\_BASED を指定した場合、または\_メッセージ\_基づいて接続した場合、 **IoConnectInterruptEx**はエラーを返します。 この動作を使用すると、Windows Vista と以前のシステムのどちらで実行しているかを判断できます。 詳細については、「 [Windows Vista より前の IoConnectInterruptEx の使用](using-ioconnectinterruptex-prior-to-windows-vista.md)」を参照してください。

 

 




