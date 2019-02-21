---
title: パラレル ポートの使用を同期します。
description: パラレル ポートの使用を同期します。
ms.assetid: ea3a1998-9e31-4047-9193-6b402db222c9
keywords:
- パラレル ポート WDK、同期
- 同期の WDK パラレル ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8c80c9b261b793a240d40d82ccfacd18bb2698
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553033"
---
# <a name="synchronizing-the-use-of-a-parallel-port"></a>パラレル ポートの使用を同期します。





クライアントは、それを使用して、終わった後にこのポートを解放する前にパラレル ポートに割り当てることによってパラレル ポートの使用を同期する必要がありますそれを使用します。

または、クライアントを選択し、(が自動的に割り当て、パラレル ポートを解放) IEEE 1284.3 デバイスの選択を解除できる − を参照してください[を選択して、IEEE 1284 デバイスに接続してパラレル ポートの選択を解除](selecting-and-deselecting-an-ieee-1284-device-attached-to-a-parallel-p.md)します。

クライアントでは、次のデバイス制御要求を使用して、割り当てし、解放パラレル ポート。

[**IOCTL\_内部\_並列\_ポート\_割り当て**](https://msdn.microsoft.com/library/windows/hardware/ff544023)

[**IOCTL\_内部\_並列\_ポート\_FREE**](https://msdn.microsoft.com/library/windows/hardware/ff544026)

カーネル モード クライアントは、システムが提供を使用しても[ポート コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544307)を使用して取得される、 [ **IOCTL\_内部\_取得\_並列\_ポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544002)要求。 この要求を返します、 [**並列\_ポート\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff544322)システム提供のコールバックに次のポインターを含む構造体。

-   **TryAllocatePort**メンバーへのポインターを[ *PPARALLEL\_お試しください\_ALLOCATE\_日常的な*](https://msdn.microsoft.com/library/windows/hardware/ff544550)コールバックで、これは、非ブロッキングのルーチンをパラレル ポートの割り当てを試みます。

-   **QueryNumWaiters**メンバーがへのポインターを[ *PPARALLEL\_クエリ\_ウェイター\_日常的な*](https://msdn.microsoft.com/library/windows/hardware/ff544532)を返すコールバックス割り当てるポートの番号とデバイス パラレル ポートの作業キューにキューに置かれた要求を選択します。

-   **FreePort**メンバーへのポインターを[ *PPARALLEL\_FREE\_ルーチン*](https://msdn.microsoft.com/library/windows/hardware/ff544509)コールバックで、パラレル ポートを解放します。

[ **IOCTL\_内部\_並列\_ポート\_ALLOCATE** ](https://msdn.microsoft.com/library/windows/hardware/ff544023)要求では、最も少ないために、クライアントによって処理システムが提供パラレル ポート関数ドライバーは、パラレル ポートが既に割り当てられている場合、クライアントの要求をキューします。 関数のドライバーのステータスで、割り当て要求が完了すると\_成功後、クライアントに、ポートを割り当てます。 クライアントは、許容できないタイムアウトの遅延またはその他デバイス固有の条件のため、いつでも、保留中の割り当て要求をキャンセルできます。

**注**   、 [ **PPARALLEL\_お試しください\_ALLOCATE\_日常的な**](https://msdn.microsoft.com/library/windows/hardware/ff544550)コールバックが直ちに返されます (は非ブロッキング)。 クライアントがのみで使用する場合、 **PPARALLEL\_お試しください\_ALLOCATE\_日常的な**パラレル ポート機能のドライバーを他のクライアントが競合している、パラレル ポートを割り当てるしようとするコールバック可能性がありますクライアントに、ポートを割り当てることはありません。 クライアントの成功を確実に並列を使用する必要がありますポートが要求を割り当てます。 (パラレル ポート関数ドライバーのキュー、およびその後プロセス、ポートの割り当てし、デバイスが、要求が受信される順序で要求を選択します)。

 

パラレル ポート機能のドライバーでは、クライアントにパラレル ポートを割り当て、クライアントがポートに排他的にアクセスします。 クライアントが呼び出す必要があります、 [ **PPARALLEL\_FREE\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff544509)ポートを解放するコールバック。 クライアントが、ポートを解放した後、パラレル ポート関数ドライバーは、いずれか、ポートの作業からキューし、要求が完了した場合 (ポート割り当てまたはデバイス選択要求)、次の要求を削除します。

クライアントを使用する必要があります、 [ **PPARALLEL\_クエリ\_ウェイター\_ルーチン**](https://msdn.microsoft.com/library/windows/hardware/ff544532)コールバック パラレル ポートを待機している他のクライアントがあるかを確認します。 一定の時間を定期的に呼び出す必要がありますのポートを割り当てることが必要なクライアント、 **PPARALLEL\_クエリ\_ウェイター\_ルーチン**を他のクライアントが待機しているかどうかを決定するコールバックポートを取得し、クライアントが待機している場合、ポートをできるだけ早く解放します。

 

 




