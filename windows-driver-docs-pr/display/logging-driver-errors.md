---
title: ドライバーのエラーのログ記録
description: ドライバーのエラーのログ記録
ms.assetid: 7deb2a9a-70aa-4660-a0c8-e118e03eef3b
keywords:
- エラー ログの WDK の表示
- WDK のエラーを表示します。
- WDK の表示エラーのログ記録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28cea0f52cff495f1f2a7fcc1fc0f849a9ce087
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347539"
---
# <a name="logging-driver-errors"></a>ドライバーのエラーのログ記録


Microsoft DirectX グラフィックスのカーネル サブシステム (*Dxgkrnl.sys*) レコードをメモリ内のログのドライバーに関連するエラー、アサーション、警告、およびイベントの表示 (で*Watchdog.sys*)。

DirectX グラフィックスのカーネル サブシステムのチェック ビルド バージョンは、既定では、ログに情報を記録に加えてエラーまたはアサーションが発生した場合に、アタッチされたデバッガーに中断されます。 によって既定では、無料のビルド バージョンの DirectX グラフィックス カーネル サブシステムのみレコード エラーとログへのアサーションと、エラーまたはアサーションが発生した場合に、デバッガーは中断されません。 この既定の動作を変更するには最初に次のレジストリを作成して\_レジストリの DWORD エントリ。

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Logging\BreakOnAssertion
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Logging\BreakOnError
```

起動エラーまたはアサーションが発生した場合、デバッガーをするためには、値を設定する必要があります**BreakOnError**または**BreakOnAssertion** 1 (TRUE) にそれぞれします。 エラーまたはアサーションが発生した場合は開始されませんデバッガーをするためには、値を設定する必要があります**BreakOnError**または**BreakOnAssertion** 0 (FALSE) にそれぞれします。

 

 





