---
title: 割り込みサービス ルーチンのパラレル ポートへの接続する
description: 割り込みサービス ルーチンのパラレル ポートへの接続する
ms.assetid: 62d3a388-6de6-4019-ab95-56b5e96d0891
keywords:
- パラレル ポート WDK、割り込みサービス ルーチン
- 割り込みサービス ルーチン WDK パラレル ポート
- 遅延ポート ルーチン WDK パラレル ポートを確認します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a631bd818cb4a3245712d59cd97c58bdf8a2c60a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573353"
---
# <a name="connecting-an-interrupt-service-routine-to-a-parallel-port"></a>割り込みサービス ルーチンのパラレル ポートへの接続する





カーネル モードのクライアントが使用できる、 [ **IOCTL\_内部\_並列\_CONNECT\_割り込み**](https://msdn.microsoft.com/library/windows/hardware/ff544020)割り込みサービス ルーチンの接続要求および*ポートをチェックするルーチンを遅延*パラレル ポート関数ドライバーの動作をします。

**注**   Microsoft クライアントが指定した割り込みルーチンを使用してお勧めしません。 割り込みの使用は、システムが不安定になる可能性があります。 既定では、IOCTL\_内部\_並列\_CONNECT\_割り込み要求が無効になっています。

 

移植および並列のデバイス用のドライバーの開発を容易には、パラレル ポートのシステムによって提供される関数のドライバーは、カーネル モードのクライアントを使用して有効にしを接続の中断要求を無効にするレジストリ フラグをサポートします。 レジストリ エントリの値によって接続の中断要求が有効になっている**EnableConnectInterruptIoctl**パラレル ポートのプラグ アンド プレイのレジストリ キーの下。 エントリの値が型 REG\_DWORD と既定値は 0x0 (無効)。 0x0 と等しくない値には、接続の中断要求が有効になります。

接続の中断要求を返します、 [**並列\_割り込み\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544290)パラレル ポートの割り込みのオブジェクトへのポインターを含む構造と、システムが提供するコールバック ルーチンに次のポインター。

-   **TryAllocatePortAtInterruptLevel**メンバーへのポインターは、非ブロッキング[ *PPARALLEL\_お試しください\_ALLOCATE\_ルーチン (ISR)* ](https://msdn.microsoft.com/library/windows/hardware/ff544328)コールバックで、カーネル モード ドライバーは、パラレル ポートを割り当てる ISR で使用できます。

-   **FreePortFromInterruptLevel**メンバーへのポインターは、非ブロッキング[ *PPARALLEL\_FREE\_ルーチン (ISR)* ](https://msdn.microsoft.com/library/windows/hardware/ff544515)コールバックをカーネル モード ドライバーは、パラレル ポートを解放する ISR で使用できます。

IRQL で割り込みサービス ルーチンと呼びますパラレル ポート上のハードウェア割り込み後 DIRQL を = です。 ドライバーが割り込みサービス ルーチンに接続されがあるかどうか、**アンロード**ドライバーを送信する必要があります、日常的な[ **IOCTL\_内部\_並列\_切断\_割り込み**](https://msdn.microsoft.com/library/windows/hardware/ff544021)要求でその**アンロード**ルーチン。

遅延ポート チェックのルーチンは、パラレル ポートが解放された後、そのポートを割り当てまたは IEEE 1284.3 デバイスを選択する保留中の要求がない場合に呼び出されます。 ドライバーは、遅延のポートのチェック ルーチンを使用して、割り込みを有効にすることができます。

クライアントに割り当てられたポートがあるない場合に、クライアントの割り込みサービス ルーチンを呼び出すと、クライアントが、PPARALLEL を呼び出すことによって、ポートを迅速に割り当てる試行できます\_お試しください\_ALLOCATE\_ルーチン (ISR) コールバック。 クライアントは、PPARALLEL を使用しても\_FREE\_ポートを解放するルーチン (ISR) コールバック。

パラレル ポートはドライバーによって共有されるため、パラレル ポート関数ドライバーは、割り込みサービス ルーチンとパラレル ポートに接続されている遅延ポート チェックのルーチンの一覧を保持します。 接続されている順序でルーチン、パラレル ポート関数ドライバーは接続割り込みルーチンとポートの遅延をすべて確認してください。

 

 




