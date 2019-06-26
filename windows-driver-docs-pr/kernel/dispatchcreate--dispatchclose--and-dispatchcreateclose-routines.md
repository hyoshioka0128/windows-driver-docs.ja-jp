---
title: DispatchCreate、DispatchClose、DispatchCreateClose ルーチン
description: DispatchCreate、DispatchClose、DispatchCreateClose ルーチン
ms.assetid: 5c1c0036-71b1-4410-b157-f9ebe3b6ecfc
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchCreate ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchClose ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchCreateClose ルーチン
- DispatchCreateClose ルーチン
- DispatchClose ルーチン
- DispatchCreate ルーチン
- Irp_mj_create 用 I/O 関数のコード
- 未完了の I/O 関数のコード
- ディスパッチ ルーチン WDK カーネルを作成します。
- ディスパッチ ルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47b259a4c10bbb28a0d7acfd246ad2058afb9f93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381720"
---
# <a name="dispatchcreate-dispatchclose-and-dispatchcreateclose-routines"></a>DispatchCreate、DispatchClose、DispatchCreateClose ルーチン





ドライバーの[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) Irp の I/O 関数のコードを持つ[ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)と[**IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)、それぞれします。 または、組み合わされた[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、これらの I/O 関数コードの両方の Irp を処理できます。

作成要求の送信元のいずれか (場合によって、アプリケーションまたはサブシステム レベル ドライバー) に代わって、デバイスを表すファイル オブジェクトを識別するハンドルを取得または呼び出しでより高度なドライバーのユーザー モード サブシステムの試行から[ **IoGetDeviceObjectPointer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceobjectpointer)または[ **IoAttachDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevice)します。

相互の終了要求は、ドライバーのデバイス オブジェクトに関連付けられたファイル オブジェクトのハンドルのユーザー モード サブシステムの終了から発生します。

これらの要求の各機能は、本質的に同期します。

 

 




