---
title: アクセス制御
description: アクセス制御
ms.assetid: 7f87276f-4014-4b37-b051-4bf02acbf575
keywords:
- 脅威を最小限に抑え、セキュリティ WDK ファイル システム
- アクセス制御の WDK ファイル システム
- アクセスの検証の WDK ファイル システム
- WDK ファイル システムのセキュリティを検証しています
- セキュリティのチェック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00ad6d5df9d0f2555f85800231a8af85eb4268c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323142"
---
# <a name="access-control"></a>アクセス制御


## <span id="ddk_access_control_if"></span><span id="DDK_ACCESS_CONTROL_IF"></span>


不適切なアクセスからの保護は、ほとんどのドライバーは、それらのデバイス オブジェクトに対して I/O マネージャーによって適用される既定のアクセス制御に依存します。 その他のメカニズムのドライバーを利用できます。 おそらく最も簡単な標準のドライバーは、ドライバーをインストールするときに、明示的なセキュリティ記述子を適用します。 デバイス オブジェクトにセキュリティ記述子を適用する例については、後のセクションで説明します。

セキュリティ ポリシーを実装するドライバーはでしたアシスタンス管理のセキュリティ アクセス用の標準の Windows Api に依存します。 この場合、ドライバーは、セキュリティ記述子の記憶域を管理し、セキュリティを検証するセキュリティの参照の監視ルーチンの呼び出しを担当します。 次などの多数のルーチンが含まれます。

-   [**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)--このルーチンは、呼び出し元のセキュリティ資格情報に対して、セキュリティ記述子を比較します。

-   [**SePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff556686)--このルーチンは、特定の権限が呼び出し元が有効である決定します。

-   [**SeSinglePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563740)--このルーチンは、呼び出し元が特定の特権が有効になっているかどうかを決定します。

-   [**SeAuditingFileOrGlobalEvents**](https://msdn.microsoft.com/library/windows/hardware/ff554778)--このルーチンは、システムが監査を有効なかどうかを示します。

-   [**SeOpenObjectAuditAlarm**](https://msdn.microsoft.com/library/windows/hardware/ff556682)--このルーチンは、開いているオブジェクトのイベントを監査します。

この一覧が完了していないが、さまざまなアクセスの検証を実行するをドライバー内で使用できる主な機能がについて説明します。

 

 




