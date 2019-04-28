---
title: ISR の登録
description: ISR の登録
ms.assetid: 903e5664-2193-4456-b133-bb979d700bdf
keywords:
- isr を特定の登録、割り込みサービス ルーチン WDK カーネル
- 割り込みオブジェクト WDK カーネルは、isr を特定の登録
- Isr WDK カーネル、isr を特定の登録
- WDK の isr を特定のカーネルを登録します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b554d7fa21a48b6806b54f1b39671f83fcb69ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382646"
---
# <a name="registering-an-isr"></a>ISR の登録


ドライバーを使用して、 [ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)登録、割り込みの ISR ルーチン。 **IoConnectInterruptEx**は Windows Vista およびそれ以降のオペレーティング システムの一部です。 **IoConnectInterruptEx**を 1 つ受け取り*パラメーター*ポインターであるパラメーターを[ **IO\_CONNECT\_割り込み\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff550541)構造体。 Windows Server 2003、Windows XP、および Windows 2000、ドライバーは、Windows Driver Kit (WDK) で含まれている Iointex.lib ライブラリを使用できます。

Windows Vista 以降、 **IoConnectInterruptEx** ISR. を登録するためのいくつかの異なるメソッドを提供します 指定された値*パラメーター*-&gt;**バージョン**メソッドを次のように決定します。

-   接続を使用して、\_行\_登録ベース、 [ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)行ベースのデバイスの割り込みのすべてのルーチン。 (デバイス、通常、ある 1 つの行に基づく割り込み多くて)。システムは、デバイスに割り当てられている任意の行ベースの割り込みを自動的に検出します。 詳細については、次を参照してください。 [、CONNECT を使用して\_行\_IoConnectInterruptEx のバージョンのベース](using-the-connect-line-based-version-of-ioconnectinterruptex.md)します。

-   接続を使用して、\_メッセージ\_登録ベース、 [ *InterruptMessageService* ](https://msdn.microsoft.com/library/windows/hardware/ff547940)すべてのデバイスのメッセージ シグナル割り込みの日常的な。 フォールバックを指定することもできます[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)ルーチン — のみの場合、デバイス、割り込みの行に基づく**IoConnectInterruptEx**登録、  *。InterruptService*ルーチン代わりにします。 システムは、デバイスに割り当てられているすべてのメッセージ シグナル割り込みを自動的に検出します。 詳細については、次を参照してください。 [、CONNECT を使用して\_メッセージ\_IoConnectInterruptEx のバージョンのベース](using-the-connect-message-based-version-of-ioconnectinterruptex.md)します。

-   接続を使用して、\_完全\_を登録する指定された、 *InterruptService*の各ルーチンを個別に中断します。 これを使用して、 *InterruptService*か、行ベースまたは、メッセージ シグナル割り込みなどがルーチンは PnP マネージャーによって渡された情報を使用して、割り込みを手動で指定する必要があります。 詳細については、次を参照してください。 [、CONNECT を使用して\_完全\_IoConnectInterruptEx のバージョンを指定した](using-the-connect-fully-specified-version-of-ioconnectinterruptex.md)します。

Windows Vista より前のオペレーティング システムで、接続を使用することができますのみ\_完全\_に指定します。 接続を指定する場合\_行\_ベースまたは CONNECT\_メッセージ\_、 **IoConnectInterruptEx**はエラーを返します。 この動作を使用すると、Windows Vista または以前のシステムで実行しているかどうかを判断します。 詳細については、次を参照してください。[を使用して IoConnectInterruptEx する前に Windows Vista](using-ioconnectinterruptex-prior-to-windows-vista.md)します。

 

 




