---
title: パラレル ポートの使用の同期
description: パラレル ポートの使用の同期
ms.assetid: ea3a1998-9e31-4047-9193-6b402db222c9
keywords:
- パラレルポート WDK、同期
- WDK パラレルポートの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ea0266896b0ce1b9acc6249173d2e99b528a33d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842316"
---
# <a name="synchronizing-the-use-of-a-parallel-port"></a>パラレル ポートの使用の同期





クライアントは、パラレルポートを使用する前にパラレルポートを割り当て、使用後にポートを解放することで、パラレルポートの使用を同期する必要があります。

また、クライアントは、IEEE 1284.3 デバイス (パラレルポートを自動的に割り当てて解放する) を選択および選択解除できます。「[パラレルポートに接続されている ieee 1284 デバイスの選択と](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)選択解除」を参照してください。

クライアントは、次のデバイス制御要求を使用して、パラレルポートの割り当てと解放を行います。

[**IOCTL\_内部\_パラレル\_ポート\_割り当て**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_port_allocate)

[**IOCTL\_内部\_パラレル\_ポート\_無料**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_port_free)

また、カーネルモードクライアントでは、システムによって提供される[パラレルポートコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を使用することもできます。これは、 [**IOCTL\_内部\_\_パラレル\_ポート\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_port_info)要求を取得します。 この要求は、システムによって提供されるコールバックへの次のポインターを含む、[**並列\_ポート\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_port_information)構造体を返します。

-   **Tryallocateport**メンバーは、 [*pparallel\_* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544550(v=vs.85))へのポインターであり、\_ルーチンコールバック\_割り当てます。これは、パラレルポートの割り当てを試みる非ブロッキングルーチンです。

-   **QueryNumWaiters**メンバーは、[*待機処理\_ルーチンコールバック\_\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_query_waiters_routine)へのポインターであり、パラレルポートの作業キューでキューに登録されているポート割り当てとデバイス選択要求の数を返します。

-   **Freeport**メンバーは、 [*PPARALLEL\_フリー\_ルーチン*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_free_routine)コールバックへのポインターであり、パラレルポートを解放します。

パラレルポートが既に割り当てられている場合、並列ポート用のシステム提供の関数ドライバーがクライアントの要求をキューに配置するため、 [**IOCTL\_内部\_パラレル\_ポート\_の割り当て**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_port_allocate)要求では、クライアントによる処理が少なくて済みます。 関数ドライバーは、ポートがクライアントに割り当てられた後、status\_status という状態の割り当て要求を完了します。 クライアントは、許容できないタイムアウト遅延またはその他のデバイス固有の状態が原因で、保留中の割り当て要求をいつでも取り消すことができます。

[**Pparallel\_TRY\_割り当て\_ルーチン**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544550(v=vs.85))コールバックが直ちに返される   に**注意**してください (は非ブロッキング)。 クライアントが**Pparallel\_** のみを使用する場合は、\_ルーチンコールバックを割り当てて、他のクライアントが競合しているパラレルポートの割り当てを試みる\_、パラレルポート関数ドライバーがクライアントにポートを割り当てないことがあります。 正常に完了するには、クライアントがパラレルポート割り当て要求を使用する必要があります。 (パラレルポート関数ドライバーはキューをキューに配置し、その後、ポート割り当てとデバイス選択の要求を受信した順序で処理します。

 

パラレルポート関数ドライバーがクライアントにパラレルポートを割り当てると、クライアントはそのポートに排他的にアクセスできるようになります。 クライアントは、 [**Pparallel\_フリー\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_free_routine)コールバックを呼び出して、ポートを解放する必要があります。 クライアントがポートを解放した後、パラレルポート関数ドライバーは、次の要求 (ポートの割り当てまたはデバイスの選択要求) をポートの作業キューから削除し、要求を完了します。

クライアントは、 [**pparallel\_クエリ\_待機処理\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_query_waiters_routine)コールバックを使用して、他のクライアントがパラレルポートを待機しているかどうかを判断する必要があります。 長時間にわたってポートを割り当てる必要があるクライアントは、 **Pparallel\_クエリ\_待機処理\_ルーチン**コールバックを定期的に呼び出して、他のクライアントがポートの取得を待機しているかどうかを確認し、クライアントが待機している場合はできるだけ早くポートを解放する必要があります。

 

 




