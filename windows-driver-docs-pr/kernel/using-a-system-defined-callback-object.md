---
title: システムによって定義されたコールバック オブジェクトの使用
description: システムによって定義されたコールバック オブジェクトの使用
ms.assetid: 1f1a2fc1-e698-41f7-84e4-9db091def690
keywords:
- コールバック オブジェクトの WDK カーネル
- システム定義のコールバック オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbfdde80eb93a862937c09c63d034c6e1f93ccf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385103"
---
# <a name="using-a-system-defined-callback-object"></a>システムによって定義されたコールバック オブジェクトの使用





システムでは、ドライバーを使用するための 3 つのコールバック オブジェクトを定義します。

**\\コールバック\\SetSystemTime**

**\\コールバック\\PowerState**

**\\コールバック\\ProcessorAdd**

登録可能性があります (たとえば、ファイル システム ドライバー) のシステム時刻を使用するドライバー、 **\\コールバック\\SetSystemTime**コールバック オブジェクト。 このコールバックは、システム時刻が変更されたときに、通知を提供します。

**\\コールバック\\PowerState**次のいずれかが発生すると、通知のコールバック オブジェクトを提供します。

-   システムは、または DC 電源 AC から切り替わります。

-   ユーザーまたはアプリケーションの要求の結果としてシステム電源ポリシーの変更。

-   システムのスリープ状態またはシャット ダウン状態に遷移が迫っていないか。 ドライバーは、シャット ダウンに応じるためにメモリにコードをロックすることができるように、通知を要求できます。 電源マネージャー、システムに送信する前に、コールバック ルーチンを通知は IRP の出力を設定します。

**\\コールバック\\ProcessorAdd**コールバックは、新しいプロセッサがシステムに追加されたときに通知を提供します。

システム定義のコールバックを使用するには、ドライバーは、属性ブロックを初期化します ([**InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes))、コールバックの名前を持つコールバック オブジェクトを表示し ([ **ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excreatecallback)) で、ドライバーの定義済みのコールバックとのみ。 ドライバーは、コールバック オブジェクトを作成することを要求する必要があります。

によって返されるハンドルを持つ**ExCreateCallback**、ドライバー呼び出し[ **ExRegisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exregistercallback)任意のコンテキストにポインターを渡すことを通知ルーチンを登録するにはそのルーチンへのポインター。 ドライバーは、いつでも、コールバック ルーチンを登録できます。 システム IRQL で登録されたコールバック ルーチンを呼び出すと、指定された条件が発生したときに&lt;= ディスパッチ\_レベル。

呼び出す必要がありますが、ドライバーでは、通知が必要なくなる、 [ **ExUnregisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exunregistercallback)登録されたコールバックの一覧から、コールバック ルーチンを削除して、コールバックへの参照を削除するにはオブジェクト。

 

 




