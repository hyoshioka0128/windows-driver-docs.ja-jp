---
title: DispatchCreate ルーチンと DispatchClose ルーチンの分離
description: DispatchCreate ルーチンと DispatchClose ルーチンの分離
ms.assetid: b2e05555-c70d-4293-8622-51eea92091b1
keywords:
- ディスパッチルーチン WDK カーネル、DispatchCreate ルーチン
- ディスパッチルーチン WDK カーネル、DispatchClose ルーチン
- DispatchClose ルーチン
- DispatchCreate ルーチン
- IRP_MJ_CREATE i/o 関数のコード
- IRP_MJ_CLOSE i/o 関数のコード
- ディスパッチルーチン WDK カーネルを作成する
- ディスパッチルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5ccca63f626ea18473555e8154f9de9a630c4df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836361"
---
# <a name="separate-dispatchcreate-and-dispatchclose-routines"></a>DispatchCreate ルーチンと DispatchClose ルーチンの分離





[**Irp\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)および[**irp\_MJ\_CLOSE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)要求のドライバーの*ディスパッチ*ルーチンでは、入力 IRP と STATUS\_SUCCESS を完了するだけでは何も行うことができません。 詳細については、「 [irp の完了](completing-irps.md)」を参照してください。

**Irp\_MJ\_CREATE**および**IRP\_\_MJ**に対する別のドライバーの*ディスパッチ*ルーチンは、基になるデバイスドライバーまたは基になるデバイスによっては、より多くの処理を実行する可能性があります。 次に、例をいくつか示します。

- クラスドライバーは、作成要求を受信すると、内部キューを初期化し、 [**IRP\_MJ\_内部\_デバイスの\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求を、デバイス構成を要求する対応するポートドライバーに送信します。コントローラーポートに対する情報または排他アクセス。

- **IRP\_MJ\_CLOSE**の受信は、ターゲットデバイスオブジェクトに関連付けられているファイルオブジェクトへの最後の参照が削除されたことを示します。 これは、ファイルオブジェクトへのすべてのハンドルが閉じられ、未処理の i/o 要求がすべて完了またはキャンセルされたことを意味します。

- 作成要求を受信すると、使用頻度の低いデバイスのドライバーが[**MmLockPagableCodeSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmlockpagablecodesection)を呼び出して、他の**IRP\_MJ\_* XXX*** 要求を処理する一部のドライバールーチンを常駐させることができます。 相互終了要求の受信時に、ドライバーは、そのようなドライバーのデバイスオブジェクトのすべてのファイルオブジェクトハンドルが閉じられたときに、ページングされたイメージセクションをページアウトすることで、システムメモリを節約するために[**MmUnlockPagableImageSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpagableimagesection)を呼び出す場合があります。

一部のドライバーでは、 **IRP\_MJ\_CLOSE**要求のみを処理します。これは、保護されたサブシステムまたは上位のドライバーによってデバイスオブジェクトが開かれた後、下位レベルのドライバーのデバイスオブジェクトがシステムに対して閉じられないためです。それ自体がシャットダウンされます。 たとえば、キーボードおよびマウスドライバーは、システムの実行中に機能する必要がある物理デバイスを表すデバイスオブジェクトを設定します。そのため、これらのドライバーは、対称の[*DispatchClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを最小にすることも、組み合わせ[*て使用することもできます。DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチン。

下位レベルのドライバーによって制御されるデバイスを、システムの実行を継続するために使用できるようにする必要がある場合、通常、ドライバーの*DispatchClose*ルーチンは呼び出されません。 たとえば、一部のシステムディスクドライバーには*DispatchClose*ルーチンがありませんが、これらのドライバーは通常、システムが次のようになる前に未処理のファイル i/o 操作を完了するための[*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを備えています。シャットダウン。

個別の[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと*DispatchClose*ルーチンを実装することができますが、ドライバーでは、作成と終了の両方の要求を処理するための[DispatchCreateClose ルーチンが1つ](a-single-dispatchcreateclose-routine.md)必要になる場合があります。

 

 




