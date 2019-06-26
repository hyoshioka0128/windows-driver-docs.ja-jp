---
title: フレームワークの外部での WDM IRP の処理
description: フレームワークの外部での WDM IRP の処理
ms.assetid: 43e1df0c-c0d1-4d41-87de-9f8f5831fb19
keywords:
- WDM Irp WDK KMDF
- WDM Irp WDK KMDF、フレームワーク外
- Irp WDK KMDF
- フレームワークの外部の Irp WDK KMDF
- I/O 要求パケット WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf651b388619750becdf41961e1b4cc5e448091d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382845"
---
# <a name="handling-wdm-irps-outside-of-the-framework"></a>フレームワークの外部での WDM IRP の処理


\[KMDF にのみ適用されます。\]

I/O マネージャーは、I/O 要求パケット (IRP) をフレームワーク ベースのドライバーに配信する際、フレームワークは IRP をインターセプトし、その後は、次のいずれか。

-   IRP を処理します。 などが含まれている Irp の処理フレームワーク[ **IRP\_MJ\_PNP** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)と[ **IRP\_MJ\_電源** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) I/O 関数のコードの主要な。 これらの Irp の処理中には、フレームワークは、ドライバーのイベントのコールバック関数を呼び出すことによってドライバーと通信可能性があります。

-   IRP のフレームワークの要求オブジェクトを作成し、ドライバーが、通常は、要求ハンドラーで受信して処理できるように、ドライバーの I/O キューのいずれかに、要求オブジェクトを提供します。 フレームワークでは、この方法で、読み取り、書き込み、およびデバイスの I/O 制御要求を処理します。

-   IRP を (には、ドライバーが、フィルター ドライバーの場合) は、次の下位ドライバーに渡すまたは完了状態のステータス値を持つ IRP\_無効な\_デバイス\_IRP に I/O が含まれているため (この場合、ドライバーは、フィルター ドライバーではありません) を要求関数コードでフレームワークがサポートされていません。

場合があります、ドライバーは、フレームワークがサポートされていない I/O 関数のコードを処理する必要があります。

まれには、ドライバーは、前に、フレームワークが処理またはドライバーが IRP の後処理フレームワークの後にする必要があり、下位レベルのドライバーでは、処理が完了したら、IRP のプリプロセスを実行する必要があります。

前処理の一部として、ドライバーは、特定の I/O キューに IRP を転送する必要があります。

次のトピックでは、このような状況について説明します。

-   [フレームワークがサポートされていない IRP の処理](handling-an-irp-that-the-framework-does-not-support.md)
-   [前処理と後処理 Irp](preprocessing-and-postprocessing-irps.md)
-   [Irp の I/O キューへのディスパッチ](dispatching-irps-to-i-o-queues.md)

 

 





