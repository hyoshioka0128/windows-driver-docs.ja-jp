---
title: 割り込みサービス ルーチンのパラレル ポートへの接続する
description: 割り込みサービス ルーチンのパラレル ポートへの接続する
ms.assetid: 62d3a388-6de6-4019-ab95-56b5e96d0891
keywords:
- パラレルポート WDK、割り込みサービスルーチン
- 割り込みサービスルーチンの WDK パラレルポート
- 遅延ポートチェックルーチン WDK パラレルポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280fa91579f4b4efd1dda3c8772dd7987dbe7274
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844803"
---
# <a name="connecting-an-interrupt-service-routine-to-a-parallel-port"></a>割り込みサービス ルーチンのパラレル ポートへの接続する





カーネルモードクライアントは、 [**IOCTL\_内部\_並列\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_connect_interrupt)して、割り込みサービスルーチンと*遅延ポートチェックルーチン*をパラレルポート関数の操作に接続するために、割り込み要求を接続\_ます。driver.

Microsoft   クライアントが指定した割り込みルーチンを使用し**ないことを**お勧めします。 割り込みを使用すると、システムが不安定になる可能性があります。 既定では、IOCTL\_INTERNAL\_PARALLEL\_CONNECT\_INTERRUPT 要求は無効になっています。

 

パラレルデバイス用のドライバーの移植と開発を容易にするために、システムによって提供されるパラレルポートの関数ドライバーは、カーネルモードのクライアントが接続割り込み要求を有効または無効にするために使用できるレジストリフラグをサポートしています。 接続割り込み要求は、プラグアンドプレイレジストリキーの下にあるレジストリエントリ値**EnableConnectInterruptIoctl**によって有効にされます。 エントリ値の型は REG\_DWORD で、既定値は 0x0 (無効) です。 0x0 と等しくない値を指定すると、接続割り込み要求が有効になります。

接続割り込み要求は、並列[ **\_割り込み\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_interrupt_information)構造体を返します。この構造には、パラレルポートの interrupt オブジェクトへのポインターと、システムによって提供されるコールバックルーチンへの次のポインターが含まれます。

-   **TryAllocatePortAtInterruptLevel**メンバーは、非ブロッキング pparallel\_へのポインターであり、 [ *\_ルーチン (isr) コールバック\_割り当て*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_try_allocate_routine)ます。これは、カーネルモードドライバーが ISR で使用してパラレルポートを割り当てることができます。

-   **FreePortFromInterruptLevel**メンバーは、非ブロッキング[*PPARALLEL\_FREE\_ルーチン (isr)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_free_routine)コールバックへのポインターであり、カーネルモードドライバーが isr で使用してパラレルポートを解放できます。

割り込みサービスルーチンは、パラレルポートのハードウェア割り込みの後、IRQL = DIRQL で呼び出されます。 ドライバーが割り込みサービスルーチンに接続し、**アンロード**ルーチンがある場合、ドライバーは、**アンロード**ルーチンで[**割り込み要求\_切断\_の内部\_並列\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_disconnect_interrupt)送信する必要があります。

遅延ポートチェックルーチンは、パラレルポートが解放された後、およびポートを割り当てたり、IEEE 1284.3 デバイスを選択したりする保留中の要求がない場合に呼び出されます。 ドライバーは、遅延ポートチェックルーチンを使用して、割り込みを有効にすることができます。

クライアントにポートが割り当てられていないときにクライアントの割り込みサービスルーチンが呼び出されると、クライアントは PPARALLEL\_呼び出して、ポートを迅速に割り当てることができます。これには、\_ルーチン (ISR) コールバック\_割り当てます。 クライアントは、PPARALLEL\_FREE\_ルーチン (ISR) コールバックを使用してポートを解放することもできます。

パラレルポートはドライバーによって共有されるため、パラレルポート関数ドライバーは、パラレルポートに接続されている割り込みサービスルーチンと遅延ポートチェックルーチンの一覧を保持します。 パラレルポート関数ドライバーは、接続されているすべての割り込みルーチンと遅延ポートチェックルーチンを接続された順序で呼び出します。

 

 




