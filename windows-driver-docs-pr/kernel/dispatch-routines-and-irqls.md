---
title: ディスパッチルーチンと IRQLs
description: ディスパッチルーチンと IRQLs
ms.assetid: fe64e0f7-3906-470a-86c5-03460e652eed
keywords:
- ディスパッチルーチン WDK カーネル、IRQLs
- IRQLs WDK ディスパッチルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4deb7576191e43829165c3c739750a6e18ab4961
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838735"
---
# <a name="dispatch-routines-and-irqls"></a>ディスパッチルーチンと IRQLs





ほとんどのドライバーのディスパッチルーチンは、IRQL = パッシブ\_レベルで任意のスレッドコンテキストで呼び出されます。ただし、次の例外があります。

-   最上位レベルのドライバーのディスパッチルーチンは、i/o 要求を発信したスレッドのコンテキストで呼び出されます。これは通常、ユーザーモードのアプリケーションスレッドです。

    つまり、ファイルシステムドライバーおよびその他の最上位レベルのドライバーのディスパッチルーチンは、IRQL = パッシブ\_レベルでは、任意のスレッドコンテキストで呼び出されます。

-   最下位レベルのデバイスドライバーの[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、および[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと、システムページングパスの上に階層化された中間ドライバーは、IRQL = APC\_レベルで、任意のスレッドコンテキスト。

    *DispatchRead*ルーチンや*DispatchWrite*ルーチン、およびこのような最下位レベルのデバイスまたは中間ドライバーで読み取り要求または書き込み要求を処理するその他のルーチンは、常に常駐している必要があります。 これらのドライバールーチンは、ページングすることも、ドライバーのページング可能なイメージセクションの一部にすることもできません。ページング可能なメモリにアクセスすることはできません。 さらに、ブロック呼び出しに依存しないようにする必要があります ( [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)のタイムアウトがゼロ以外の場合など)。

-   休止状態またはページングパス内のドライバーの[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、IRQL = ディスパッチ\_レベルで呼び出すことができます。 このようなドライバーの[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、[**デバイス\_使用状況\_通知**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-device-usage-notification)要求に\_て、PnP IRP\_処理できるように準備する必要があります。

-   起動時に突入電流電源を必要とするドライバーの*DispatchPower*ルーチンは、IRQL = ディスパッチ\_レベルで呼び出すことができます。

詳細については、「[ハードウェアの優先順位の管理](managing-hardware-priorities.md)」を参照してください。

 

 




