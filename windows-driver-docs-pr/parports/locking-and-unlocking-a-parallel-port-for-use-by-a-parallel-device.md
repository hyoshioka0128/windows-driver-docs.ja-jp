---
title: ロックおよびパラレル ポートのロックを解除
description: パラレル デバイスに使用するパラレル ポートのロックとロック解除
ms.assetid: dbfa962e-9de8-4a9c-b962-24b53c41f35d
keywords:
- 並列デバイス WDK、ポートのロック/ロック解除
- WDK の並列のデバイスをロック
- パラレル ポートのロックを解除します。
- 中断せずに操作 WDK 並列デバイス
- パラレル ポートの解放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cef7f6c2e1e07b3077695d49892fb3c3cfdeeb68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373537"
---
# <a name="locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device"></a>パラレル デバイスに使用するパラレル ポートのロックとロック解除





並列デバイス上の操作の中断のないシーケンスを実行するには、クライアントはパラレル ポートを割り当てるし、ポートで IEEE 1284.3 デバイスを選択する必要があります。 一連の操作には、I/O 要求を完了して、パラレル ポート バス ドライバーによって提供されるコールバック ルーチンの実行を含めることができます。 一連の操作を完了すると、クライアントが IEEE 1284.3 デバイスの選択を解除し、親のパラレル ポートを解放する必要があります。

パラレル ポートのシステム提供のバス ドライバーには、ロックおよびパラレル ポートのロックを解除する次の内部デバイス制御の要求がサポートされています。

[**IOCTL\_内部\_ロック\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff544009)

[**IOCTL\_内部\_ロック\_ポート\_いいえ\_を選択します**](https://msdn.microsoft.com/library/windows/hardware/ff544014)

[**IOCTL\_内部\_UNLOCK\_ポート**](https://msdn.microsoft.com/library/windows/hardware/ff544056)

[**IOCTL\_内部\_UNLOCK\_ポート\_いいえ\_選択解除**](https://msdn.microsoft.com/library/windows/hardware/ff544060)

Microsoft は、クライアントがロックのポートを使用して、ポートの要求のみにこれらの要求を提供する機能を使用して、デバイスを操作できる場合のロックを解除ことをお勧めします。 それ以外の場合、クライアントが select にはロック ポートの使用できるし、ロックが解除要求をポートありません。 これにより、クライアント、IEEE 1284.3 デイジー チェーン仕様に準拠していない、選択と選択解除メカニズムを使用するデバイスを操作する柔軟性が高まります。 クライアントは、ポートを割り当てる選択を要求しないロック ポートを使用できを使用して、デバイスを動作[並列のデバイスのデバイスのコントロール要求](https://msdn.microsoft.com/library/windows/hardware/ff543945)と[デバイス コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544275)します。

クライアントは、並列のデバイスをロックして、パラレル ポート、パラレル ポート バス ドライバー ポートは、クライアントの間で共有を管理するためのロックを解除する必要はありませんを個々 の I/O 要求を送信できます。 パラレル ポート バス ドライバーは、I/O 要求を処理し、ポートを待機しているクライアントがある場合は、I/O 要求の完了後すぐにポートを解放する直前にパラレル ポートを自動的に割り当てます。

パラレル ポート バス ドライバーは、ポートを割り当てることができる場合並列デバイス セットのタイムアウト時間内に、期間、デバイスのワーカー スレッドは要求を完了します。 パラレル ポート バス ドライバーのステータスの保留中の要求が完了するとそれ以外の場合、\_デバイス\_ビジーです。

 

 




