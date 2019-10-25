---
title: パラレルポートのロックとロック解除
description: パラレル デバイスに使用するパラレル ポートのロックとロック解除
ms.assetid: dbfa962e-9de8-4a9c-b962-24b53c41f35d
keywords:
- パラレルデバイス WDK、ポートロック/ロック解除
- WDK パラレルデバイスのロック
- パラレルポートのロック解除
- 中断のないオペレーション WDK 並列デバイス
- パラレルポートの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a95404992ea7af6cca6ce7ebe96b90d0517060a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845315"
---
# <a name="locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device"></a>パラレル デバイスに使用するパラレル ポートのロックとロック解除





並列デバイスで中断されていない一連の操作を実行するには、クライアントがパラレルポートを割り当て、ポートで IEEE 1284.3 デバイスを選択する必要があります。 一連の操作には、i/o 要求を完了し、パラレルポートバスドライバーによって提供されるコールバックルーチンを実行することができます。 一連の操作が完了したら、クライアントは IEEE 1284.3 デバイスの選択を解除し、親パラレルポートを解放する必要があります。

パラレルポート用のシステム提供のバスドライバーでは、次の内部デバイス制御要求を使用して、パラレルポートのロックとロック解除を行うことができます。

[**IOCTL\_内部\_ロック\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_lock_port)

[**IOCTL\_内部\_ロック\_ポート\_\_選択なし**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_lock_port_no_select)

[**IOCTL\_内部\_\_ポートのロック解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_unlock_port)

[**IOCTL\_内部\_\_\_ポートのロック解除\_オフ選択解除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_unlock_port_no_deselect)

クライアントは、これらの要求によって提供される機能のみを使用してデバイスを操作できる場合は、ロックポートを使用し、ポート要求のロックを解除することをお勧めします。 そうしないと、クライアントはロックポート no select および lock port no 非選択要求を使用できます。 これにより、クライアントは、IEEE 1284.3 デイジーチェーンの仕様に準拠していない選択および deselection メカニズムを使用するデバイスを柔軟に操作できるようになります。 クライアントは、ポートの割り当てにポートを選択せずにロックすることができます。その後、デバイスは、デバイス制御要求を使用して[並列デバイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)と[並列デバイスコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)によって操作します。

クライアントはパラレルポートをロックおよびロック解除することなく、並列デバイスに個々の i/o 要求を送信できます。これは、パラレルポートバスドライバーがクライアント間でのポート共有を管理するためです。 パラレルポートバスドライバーは、i/o 要求を処理する直前にパラレルポートを自動的に割り当て、ポートを待機しているクライアントがある場合は、i/o 要求の完了直後にポートを解放します。

パラレルポートバスドライバーが、設定されたタイムアウト期間内にポートを並列デバイスに割り当てることができる場合は、デバイスのワーカースレッドが要求を完了します。 そうしないと、パラレルポートバスドライバーは、状態が デバイスの\_ビジー状態で\_保留中の要求を完了します。

 

 




