---
title: IRP の主要な関数コード
description: IRP の主要な関数コード
ms.date: 03/09/2020
ms.assetid: 11c5b1a9-74c0-47fb-8cce-a008ece9efae
ms.localizationpriority: medium
ms.openlocfilehash: 17cb9101cc034c0f1cd58b7142c4c70750284793
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2020
ms.locfileid: "78935391"
---
# <a name="irp-major-function-codes"></a>IRP の主要な関数コード


各[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)のドライバー固有の i/o スタックの場所 ([**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)) には、主な関数コード (IRP_MJ_XXX) が含まれています。これにより、ドライバーは、i/o 要求を満たすためにどのような操作を実行するか、または基になるデバイスドライバーに対して実行するかを指定します。 各カーネルモードドライバーは、サポートする必要がある主要な関数コードのディスパッチルーチンを提供する必要があります。

特定の**irp\_MJ\_<em>XXX</em>** コードで実行される特定の操作は、基になるデバイスによって多少異なります。特に、 [**irp\_MJ\_デバイス\_control**](irp-mj-device-control.md)および[**irp\_MJ\_内部\_デバイス\_制御**](irp-mj-internal-device-control.md)要求に依存します。 たとえば、キーボードドライバーに送信される要求は、必ずしもディスクドライバーに送信される要求とは多少異なることがあります。 ただし、i/o マネージャーは、システム定義の主要な関数コードごとに、パラメーターと i/o スタックの場所の内容を定義します。

上位レベルのすべてのドライバーは、次の下位レベルのドライバーに対して Irp 内に適切な i/o スタックの場所を設定し、各入力 IRP で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すか、またはドライバーによって作成された irp (上位レベルのドライバーが入力 irp に保持している場合) を呼び出します。 そのため、すべての中間ドライバーは、基になるデバイスドライバーが処理する主要な関数コードごとにディスパッチルーチンを提供する必要があります。 そうしないと、アプリケーションまたは上位レベルのドライバーが、基になるデバイスドライバーに i/o 要求を送信しようとするたびに、新しい中間ドライバーが "チェーンを中断" します。

また、ファイルシステムドライバーでは **\_\_<em>XXX</em>**  、システム定義の**irp\_MJ\_<em>xxx</em>** 関数コードに必要なサブセットが処理されます

ドライバーは、次の主要な関数コードの一部またはすべてで設定された Irp を処理します。

[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)

[**IRP\_MJ\_閉じる**](irp-mj-close.md)

[**IRP\_MJ\_作成**](irp-mj-create.md)

[**IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IRP\_MJ\_フラッシュ\_バッファー**](irp-mj-flush-buffers.md)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_の電源**](irp-mj-power.md)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**IRP\_MJ\_読み取り**](irp-mj-read.md)

[**IRP\_MJ\_設定\_情報**](irp-mj-set-information.md)

[**IRP\_MJ\_シャットダウン**](irp-mj-shutdown.md)

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

[**IRP\_MJ\_書き込み**](irp-mj-write.md)

このセクションで説明する入力パラメーターと出力パラメーターは、IRP 内の関数固有のパラメーターです。

Irp の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。

 

 




