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
ms.openlocfilehash: 556036d7912104cbdf448345a125711f9355bcfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381772"
---
# <a name="access-control"></a>アクセス制御


## <span id="ddk_access_control_if"></span><span id="DDK_ACCESS_CONTROL_IF"></span>


不適切なアクセスからの保護は、ほとんどのドライバーは、それらのデバイス オブジェクトに対して I/O マネージャーによって適用される既定のアクセス制御に依存します。 その他のメカニズムのドライバーを利用できます。 おそらく最も簡単な標準のドライバーは、ドライバーをインストールするときに、明示的なセキュリティ記述子を適用します。 デバイス オブジェクトにセキュリティ記述子を適用する例については、後のセクションで説明します。

セキュリティ ポリシーを実装するドライバーはでしたアシスタンス管理のセキュリティ アクセス用の標準の Windows Api に依存します。 この場合、ドライバーは、セキュリティ記述子の記憶域を管理し、セキュリティを検証するセキュリティの参照の監視ルーチンの呼び出しを担当します。 次などの多数のルーチンが含まれます。

-   [**SeAccessCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck)--このルーチンは、呼び出し元のセキュリティ資格情報に対して、セキュリティ記述子を比較します。

-   [**SePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-seprivilegecheck)--このルーチンは、特定の権限が呼び出し元が有効である決定します。

-   [**SeSinglePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-sesingleprivilegecheck)--このルーチンは、呼び出し元が特定の特権が有効になっているかどうかを決定します。

-   [**SeAuditingFileOrGlobalEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-seauditingfileorglobalevents)--このルーチンは、システムが監査を有効なかどうかを示します。

-   [**SeOpenObjectAuditAlarm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-seopenobjectauditalarm)--このルーチンは、開いているオブジェクトのイベントを監査します。

この一覧が完了していないが、さまざまなアクセスの検証を実行するをドライバー内で使用できる主な機能がについて説明します。

 

 




