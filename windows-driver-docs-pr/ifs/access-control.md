---
title: ドライバーのアクセス制御
description: ドライバーは、アクセス制御によって不適切なアクセスから保護します。
ms.assetid: 7f87276f-4014-4b37-b051-4bf02acbf575
keywords:
- セキュリティ WDK ファイルシステム、脅威の最小化
- アクセス制御 WDK ファイルシステム
- 検証 WDK ファイルシステムへのアクセス
- セキュリティ WDK ファイルシステムの検証
- セキュリティの確認
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f40be2d65b141524f1aed5c567ca0f0d14e8ede8
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949742"
---
# <a name="access-control-in-a-driver"></a>ドライバーのアクセス制御

不適切なアクセスから保護するために、ほとんどのドライバーは、デバイスオブジェクトに対して i/o マネージャーによって適用される既定のアクセス制御に依存しています。 ドライバーでは、他のメカニズムを使用できます。 通常は、ドライバーをインストールするときに、明示的なセキュリティ記述子を適用するのが最も簡単です。 デバイスオブジェクトにセキュリティ記述子を適用する例については、後のセクションで説明します。

独自のセキュリティポリシーを実装するドライバーは、標準の Windows Api に依存して、セキュリティアクセスの管理を支援することができます。 この場合、ドライバーはセキュリティ記述子の格納を管理し、セキュリティを検証するためにセキュリティ参照モニタールーチンを呼び出します。 これには、次のような多くのルーチンが含まれます。

- [**Seaccesscheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)--このルーチンは、セキュリティ記述子を呼び出し元のセキュリティ資格情報と比較します。

- [**SePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seprivilegecheck)--このルーチンは、指定された特権が呼び出し元に対して有効になっているかどうかを判断します。

- [**SeSinglePrivilegeCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-sesingleprivilegecheck)--このルーチンは、呼び出し元に対して特定の特権が有効になっているかどうかを判断します。

- [**SeAuditingFileOrGlobalEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seauditingfileorglobalevents)--このルーチンは、システムで監査が有効になっているかどうかを示します。

- [**SeOpenObjectAuditAlarm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seopenobjectauditalarm)--このルーチンは、開いているオブジェクトイベントを監査します。

この一覧は完全ではありませんが、アクセス検証を実行するためにドライバー内で使用できる主な機能をいくつか説明しています。
