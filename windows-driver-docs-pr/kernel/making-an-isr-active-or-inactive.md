---
title: ISR をアクティブまたは非アクティブにする
description: Windows 8 以降、ドライバーは、アクティブまたは非アクティブに登録されている割り込みサービス ルーチン (ISR) IoReportInterruptActive または IoReportInterruptInactive ルーチンを呼び出すことができます。
ms.assetid: 788D9341-D1F8-4126-8C30-AA49DE27F4BB
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6dfb0b4a3e803d2368dbc0657cebf0df5d00f12d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378740"
---
# <a name="making-an-isr-active-or-inactive"></a>ISR をアクティブまたは非アクティブにする


Windows 8 以降、ドライバーが呼び出すことができます、 [ **IoReportInterruptActive** ](https://msdn.microsoft.com/library/windows/hardware/jj158875)または[ **IoReportInterruptInactive** ](https://msdn.microsoft.com/library/windows/hardware/jj158876)ルーチンを作成します。登録済みの割り込みサービス ルーチン (ISR) アクティブまたは非アクティブです。

ISR、登録と、割り込みまたは割り込みのセットに ISR を接続するには、ドライバーの呼び出し、 [ **IoConnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548378)ルーチン。 ドライバーを使用できる ISR が登録されると、 **IoReportInterruptActive**と**IoReportInterruptInactive**を実行する軽量の (または「ソフト」) 接続および切断の ISR のままにする操作登録が変更されていません。 **IoReportInterruptInactive**関連の中断や割り込みの論理的な切断することで、ISR への呼び出しを無効にします。 **IoReportInterruptActive** ISR への呼び出しを有効にするには、これら割り込みの論理的な接続

たとえば、ドライバーを呼び出す**IoReportInterruptInactive**ソフト-切断する一連の割り込みのデバイスが、D0 電源の状態と呼び出しを終了する前に**IoReportInterruptActive**これらソフト-接続するにはデバイスが D0 を再入力した後に中断します。 原則として、ドライバーを呼び出すことが代わりに[ **IoDisconnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549093) D0、および呼び出し、デバイスが終了する前に**IoConnectInterruptEx**デバイス入ります D0 後。 ただし、 **IoReportInterrupt * Xxx*** 呼び出しより高速**IoConnectInterruptEx**と**IoDisconnectInterruptEx**呼び出し。 対照的に**IoConnectInterruptEx**と**IoDisconnectInterruptEx**呼び出しで、さまざまな理由 (たとえば、十分なシステム リソース) が失敗する可能性があります、 **IoReportInterrupt * Xxx*** 呼び出し失敗する場合、これまでは、ほとんどありません。 さらに、 **IoReportInterrupt * Xxx*** IRQL でルーチンを呼び出すことができます&lt;= ディスパッチ\_レベルに対し、 **IoConnectInterruptEx**と**IoDisconnectInterruptEx**パッシブでのみ呼び出すことができます\_レベル。

既定では、ISR はアクティブな (および ISR への呼び出しが有効になっている) の後**IoConnectInterruptEx** ISR を正常に登録します。

呼び出す**IoReportInterruptInactive**と**IoReportInterruptActive**は省略可能です。 ドライバー呼び出されるまで、登録されている ISR をアクティブに保つ場合は、ドライバーは、これらのルーチンを呼び出すことはありません、 [ **IoDisconnectInterruptEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549093) ISR の登録を解除するルーチン

ドライバーは、これらの割り込みの ISR がアクティブな場合にのみ、割り込みを発行するデバイスを構成する必要があります。 デバイスが ISR がアクティブでない場合は、割り込みを発行するを防ぐために失敗は、システムが不安定になる可能性があります。 たとえば、デバイスは、その他のデバイスと割り込みのレベルによってトリガーされる行を共有すると、デバイスの問題は、ISR がアクティブでないときに要求を中断、行の他のデバイスの isr を特定は認識しません割り込みと割り込みを発生させるのには引き続き. 呼び出しの前に**IoReportInterruptInactive**ドライバーは、割り込みの発行を停止するデバイスを構成する必要があります。 呼び出した後**IoReportInterruptActive**ドライバーは、割り込みの発行を実行するデバイスを構成する必要があります。

登録を解除するには、ISR するドライバーを呼び出すことができます**IoDisconnectInterruptEx** ISR が現在アクティブまたは非アクティブかどうかに関係します。

**IoReportInterruptActive** ISR が既にアクティブなときに発生する呼び出しは、影響を与えませんが、エラーとしては扱われません。 同様に、 **IoReportInterruptInactive** ISR が既にアクティブでない場合に発生する呼び出しは、影響を与えませんが、エラーとしては扱われません。

 

 




