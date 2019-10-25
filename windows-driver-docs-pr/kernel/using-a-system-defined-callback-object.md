---
title: システムによって定義されたコールバック オブジェクトの使用
description: システムによって定義されたコールバック オブジェクトの使用
ms.assetid: 1f1a2fc1-e698-41f7-84e4-9db091def690
keywords:
- コールバックオブジェクト WDK カーネル
- システム定義のコールバックオブジェクトの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e5686dd3a37f86e8a2a8db7f87d162eac5c785e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836024"
---
# <a name="using-a-system-defined-callback-object"></a>システムによって定義されたコールバック オブジェクトの使用





システムは、ドライバーで使用する3つのコールバックオブジェクトを定義します。

**\\コールバック\\SetSystemTime**

**\\コールバック\\PowerState**

**\\コールバック\\ProcessorAdd**

システム時刻 (ファイルシステムドライバーなど) を使用するドライバーは、 **\\コールバック\\SetSystemTime**コールバックオブジェクトに登録できます。 このコールバックは、システム時刻が変更されたときの通知を提供します。

次のいずれかが発生した場合に通知を行うために、 **\\コールバック\\PowerState** callback オブジェクトによって提供されます。

-   システムは AC 電源から DC 電源へ、またはその逆に切り替わります。

-   システムの電源ポリシーは、ユーザーまたはアプリケーションの要求の結果として変更されます。

-   システムのスリープ状態またはシャットダウン状態への移行は、間もなく終了します。 ドライバーは、シャットダウンを見越してコードをメモリにロックできるように通知を要求できます。 コールバックルーチンは、電源マネージャーがシステム設定-電源 IRP を送信する前に通知されます。

新しいプロセッサがシステムに追加されると、 **\\コールバック\\ProcessorAdd**コールバックによって通知が提供されます。

システム定義のコールバックを使用するために、ドライバーは、ドライバー定義のコールバックの場合と同様に、コールバックの名前を使用して属性ブロック ([**Initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)) を初期化し、コールバックオブジェクト ([**ExCreateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)) を開きます。 ドライバーは、コールバックオブジェクトを作成するように要求することはできません。

**ExCreateCallback**によって返されるハンドルを使用すると、ドライバーは[**exregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exregistercallback)を呼び出して通知ルーチンを登録し、任意のコンテキストへのポインターとルーチンへのポインターを渡します。 ドライバーは、いつでもコールバックルーチンを登録できます。 指定された条件が発生すると、システムは IRQL&lt;= ディスパッチ\_レベルで登録されているコールバックルーチンを呼び出します。

ドライバーが通知を必要としなくなった場合は、 [**Exunregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exunregistercallback)を呼び出して、登録されているコールバックの一覧からコールバックルーチンを削除し、コールバックオブジェクトへの参照を削除する必要があります。

 

 




