---
title: DispatchCreate ルーチンと DispatchClose ルーチンの分離
description: DispatchCreate ルーチンと DispatchClose ルーチンの分離
ms.assetid: b2e05555-c70d-4293-8622-51eea92091b1
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchCreate ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchClose ルーチン
- DispatchClose ルーチン
- DispatchCreate ルーチン
- Irp_mj_create 用 I/O 関数のコード
- 未完了の I/O 関数のコード
- ディスパッチ ルーチン WDK カーネルを作成します。
- ディスパッチ ルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04c19f7f3261b5e3a2aa9f8afedb146996e1699c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386581"
---
# <a name="separate-dispatchcreate-and-dispatchclose-routines"></a>DispatchCreate ルーチンと DispatchClose ルーチンの分離





ドライバーの*ディスパッチ*ルーチン[ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)と[ **IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)要求可能性があります何もしない複数の完全な入力の状態が IRP\_成功します。 詳細については、次を参照してください。 [Irp の完了](completing-irps.md)します。

別のドライバーの*ディスパッチ*ルーチン**IRP\_MJ\_作成**と**IRP\_MJ\_閉じる**要求基になるデバイス ドライバーによって、または基になるデバイスに複数の作業を行う可能性があります。 次に、例をいくつか示します。

- 作成要求の受信後は、クラス ドライバー可能性があります、内部キューを初期化し、送信、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)デバイスの構成情報またはコント ローラーのポートへの排他アクセスを要求に対応するポート ドライバーに要求します。

- 受信確認の**IRP\_MJ\_閉じる**ターゲット デバイス オブジェクトに関連付けられているファイル オブジェクトへの最後の参照が削除されていることを示します。 つまり、ファイル オブジェクトに対してすべてのハンドルが閉じられたこととすべての未処理 I/O 要求が完了またはキャンセルされました。

- 作成要求の受信後、使用頻度の低いデバイスのドライバーを呼び出すことができます[ **MmLockPagableCodeSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmlockpagablecodesection)他を処理するドライバー ルーチンの一部に常駐していることを**IRP\_MJ\_* XXX*** 要求。 終了要求を逆方向の要求を受信するには、ドライバーを呼び出すことができます[ **MmUnlockPagableImageSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunlockpagableimagesection)のページング可能なイメージ セクションのすべてのファイル オブジェクトのハンドルのときにページ アウトすることでシステム メモリを節約するためにこのようなドライバーのデバイス オブジェクトが閉じられます。

一部のドライバーが処理**IRP\_MJ\_閉じる**のため対称に対してのみ要求によって保護されたサブシステムまたは上位レベルのドライバーは下位レベルのドライバーのデバイスのデバイス オブジェクトを開いた後、システム自体がシャット ダウンされるまでオブジェクトが閉じられていません。 たとえば、キーボードとマウスのドライバーを設定する必要がある機能、システムが実行中にこれらのドライバーが最小限に抑える必要がありますので、物理デバイスを表すデバイス オブジェクトする[ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)対称ルーチンと結合がある可能性がありますまたは[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

かどうか下位レベルのドライバーによって制御されるデバイスが、システム、ドライバーの実行を続行可能にする必要があります*DispatchClose*ルーチン一般的には呼び出されません。 たとえば、一部のシステム ディスク ドライバーされていない*DispatchClose*ルーチンが、これらのドライバーが通常が[ *DispatchFlushBuffers* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンをシステムがシャット ダウンする前に、すべての未処理 i/o 操作を完了します。

実装するときに分離[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と*DispatchClose*ルーチン、ドライバーがある場合があります[単一 DispatchCreateClose ルーチン](a-single-dispatchcreateclose-routine.md)両方を処理するため作成し、要求を閉じます。

 

 




