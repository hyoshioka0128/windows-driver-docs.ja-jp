---
title: システムによって定義されたコールバック オブジェクトの使用
description: システムによって定義されたコールバック オブジェクトの使用
ms.assetid: 1f1a2fc1-e698-41f7-84e4-9db091def690
keywords:
- コールバック オブジェクトの WDK カーネル
- システム定義のコールバック オブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f563c5a5327ac8eeb02d9a0efb55bc6adc995880
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361123"
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

システム定義のコールバックを使用するには、ドライバーは、属性ブロックを初期化します ([**InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804))、コールバックの名前を持つコールバック オブジェクトを表示し ([ **ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)) で、ドライバーの定義済みのコールバックとのみ。 ドライバーは、コールバック オブジェクトを作成することを要求する必要があります。

によって返されるハンドルを持つ**ExCreateCallback**、ドライバー呼び出し[ **ExRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff545534)任意のコンテキストにポインターを渡すことを通知ルーチンを登録するにはそのルーチンへのポインター。 ドライバーは、いつでも、コールバック ルーチンを登録できます。 システム IRQL で登録されたコールバック ルーチンを呼び出すと、指定された条件が発生したときに&lt;= ディスパッチ\_レベル。

呼び出す必要がありますが、ドライバーでは、通知が必要なくなる、 [ **ExUnregisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff545649)登録されたコールバックの一覧から、コールバック ルーチンを削除して、コールバックへの参照を削除するにはオブジェクト。

 

 




