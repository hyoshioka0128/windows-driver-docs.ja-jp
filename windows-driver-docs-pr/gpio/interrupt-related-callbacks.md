---
title: 割り込み関連のコールバック
description: オプションとして、汎用入出力 (GPIO) コント ローラーのドライバーは、GPIO 割り込みのサポートを提供できます。
ms.assetid: 638B52A0-CB8D-4A79-B7D1-ED2474E46DAE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 755abefdf6f0d1e866d6f00c883eaac5cbbf451d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578229"
---
# <a name="interrupt-related-callbacks"></a>割り込み関連のコールバック


オプションとして、汎用入出力 (GPIO) コント ローラーのドライバーは、GPIO 割り込みのサポートを提供できます。 GPIO 割り込みをサポートするためには、GPIO コント ローラーのドライバーは、これらの割り込みを管理するコールバック関数のセットを実装します。 ドライバーには、GPIO フレームワークの拡張機能 (GpioClx) のクライアントとして自身を登録するときに、ドライバーが提供する登録パケット内のこれらのコールバック関数へのポインターが含まれています。 この登録パケットの詳細については、次を参照してください。 [ **GPIO\_クライアント\_登録\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh439479)します。

原則としては、チップ (SoC) チップでのシステムの一部として統合されている GPIO コント ローラーは、SoC チップでのプロセッサによって直接アクセスできるメモリ マップト ハードウェア レジスタを持ちます。 ただし、GPIO コント ローラーは別のデバイス可能性がありますに接続する外部 SoC チップを介してシリアル バスでは、次の図に示すように。

![統合の gpio コント ローラーと外部の gpio コント ローラー](images/gpioconnects.png)

この図では、外部の GPIO コント ローラーは I²C バスに接続されます。 このバスは、SoC、チップの一部として統合されて I²C バス コント ローラーによって制御されます。 外部の GPIO コント ローラーからの割り込み要求行は、統合の GPIO コント ローラー上のピンに接続されます。 [GpioClx DDI](https://msdn.microsoft.com/library/windows/hardware/hh439456)統合 GPIO コント ローラーとこの例では、外部の GPIO コント ローラーの両方に対応できます。

GPIO コント ローラーのデバイスがメモリ マップされている場合は、GPIO コント ローラーのドライバーは DIRQL でコント ローラーのハードウェア レジスタを直接アクセスできます。 ただし、GPIO コント ローラーが順番に接続されている場合、GPIO コント ローラー ドライバー アクセス IRQL でのみハードウェア レジスタ = パッシブ\_レベルで説明したよう[パッシブ レベル Isr](https://msdn.microsoft.com/library/windows/hardware/hh698262)します。

持つメモリ マップト ハードウェア GPIO コント ローラーの登録のドライバーを設定する必要があります、 **MemoryMappedController** GpioClx にドライバーを提供するデバイス情報でフラグ ビットです。 GpioClx がハードウェア レジスタはメモリ マップがないと IRQL でのみ登録、ドライバーがこれらをアクセスできることを想定するそれ以外の場合、パッシブ =\_レベル。 このフラグのビットの詳細については、次を参照してください。 [**コント ローラー\_属性\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/hh439449)します。

GpioClx では、GPIO コント ローラーから割り込み要求を処理する割り込みサービス ルーチン (ISR) を実装します。 この ISR では、次の割り込みに関連するコールバック関数を呼び出します。

[*クライアント\_ClearActiveInterrupts*](https://msdn.microsoft.com/library/windows/hardware/hh439341)
[*クライアント\_MaskInterrupts* ](https://msdn.microsoft.com/library/windows/hardware/hh439380) 
 [ *クライアント\_QueryActiveInterrupts*](https://msdn.microsoft.com/library/windows/hardware/hh439395)
[*クライアント\_QueryEnabledInterrupts* ](https://msdn.microsoft.com/library/windows/hardware/dn265184) 
[*クライアント\_UnmaskInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh439435) DIRQL またはパッシブのいずれかでこれらの関数を呼び出す\_DIRQL で GpioClx の ISR を実行するかどうかに応じて、レベル、またはパッシブ\_レベル。 場合は、ISR で DIRQL でこれらの関数が呼び出す**MemoryMappedController** = 1、およびパッシブ\_レベル**MemoryMappedController** = 0。 いずれの場合も、ISR 自動的にシリアル化のコールバックにこれらの関数のもう 1 つの呼び出しの途中でこれらの関数の 1 つの呼び出しは行われないようにします。

GPIO フレームワークの拡張機能がパッシブにのみ、次の割り込みに関連するコールバック関数を呼び出す\_かどうかに関係なく、レベル、 **MemoryMappedController** フラグの設定。

[*クライアント\_DisableInterrupt*](https://msdn.microsoft.com/library/windows/hardware/hh439371)
[*クライアント\_EnableInterrupt* ](https://msdn.microsoft.com/library/windows/hardware/hh439377)場合、 **MemoryMappedController**フラグが設定されていない、すべての割り込みに関連するコールバック関数はパッシブで呼び出されます\_レベル。 GpioClx は、これらの関数のもう 1 つの呼び出しの途中でこれらの関数の 1 つの呼び出しが行われないように、これらの関数の呼び出しを自動的にシリアル化します。

ただし場合、 **MemoryMappedController**フラグが設定されて、*クライアント\_EnableInterrupt*と*クライアント\_DisableInterrupt*関数必要があります明示的に同期の割り込みの有効化し DIRQL で他の 4 つの割り込みに関連するコールバック関数を呼び出す GpioClx ISR に操作を無効にします。

通常、他<em>クライアント\_</em>Xxx コールバック関数 (名前にが含まれていません"*割り込み*") 割り込みに関連する処理を実行しないと、そのため、同期させる必要はありませんGpioClx ISR に ただし、いずれかの場合これらの関数がパッシブで呼び出されます\_レベルと DIRQL に割り込み関連の関数によってアクセスされる割り込み設定にアクセスするコードを含めることが、このコードは、ISR に同期する必要があります

割り込みの同期をサポートするためには、GpioClx は、一連の割り込みのロックを実装します。 パッシブで実行されているコールバック関数\_レベルを呼び出すことができます、 [ **GPIO\_CLX\_AcquireInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh439482)割り込みのロックを取得するメソッドを呼び出すと、[ **GPIO\_CLX\_ReleaseInterruptLock** ](https://msdn.microsoft.com/library/windows/hardware/hh439494)ロックを解放するメソッド。 関数は、割り込みのロックを保持しているときに、GpioClx ISR を実行できず、この ISR、割り込みに関連するコールバック関数を呼び出すことはできません。 迅速に処理する GPIO 割り込みを有効にするには、ドライバーする必要があります、割り込みに対してロックを保持されなくが必要です。

詳細については、次を参照してください。 [GPIO コント ローラーのドライバーの同期を中断](https://msdn.microsoft.com/library/windows/hardware/jj851070)します。

 

 




