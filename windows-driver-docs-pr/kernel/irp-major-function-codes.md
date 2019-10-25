---
title: IRP の主要な関数コード
description: IRP の主要な関数コード
ms.date: 08/12/2017
ms.assetid: 11c5b1a9-74c0-47fb-8cce-a008ece9efae
ms.localizationpriority: medium
ms.openlocfilehash: e89c464ff82bfa3834501b54a2c1a8796087164b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838610"
---
# <a name="irp-major-function-codes"></a>IRP の主要な関数コード





それぞれのドライバー固有の i/o スタックの場所 (**IO\_スタック**は、サポートする必要がある主要な関数コードの場所\_ます。

特定の**irp\_MJ\_<em>XXX</em>** コードが実行する特定の操作は、基になるデバイスによって多少異なります。特に、 [**irp\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)および[**IRP\_MJ @no内部\_デバイス\_制御要求を管理する (_s)** ](irp-mj-internal-device-control.md) 。 たとえば、キーボードドライバーに送信される要求は、必ずしもディスクドライバーに送信される要求とは多少異なることがあります。 ただし、i/o マネージャーは、システム定義の主要な関数コードごとに、パラメーターと i/o スタックの場所の内容を定義します。

上位レベルのすべてのドライバーは、次の下位レベルのドライバーに対して Irp 内に適切な i/o スタックの場所を設定し、各入力 IRP で[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出すか、またはドライバーによって作成された irp (上位レベルのドライバーが入力 irp に保持している場合) を呼び出します。 そのため、すべての中間ドライバーは、基になるデバイスドライバーが処理する主要な関数コードごとにディスパッチルーチンを提供する必要があります。 そうしないと、アプリケーションまたは上位レベルのドライバーが、基になるデバイスドライバーに i/o 要求を送信しようとするたびに、新しい中間ドライバーが "チェーンを中断" します。

また、ファイルシステムドライバーでは **\_\_**  、システム定義の**irp\_MJ\_<em>xxx</em>** 関数コードに必要なサブセットが処理されます

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

 

 




