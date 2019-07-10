---
title: IRP の主要な関数コード
description: IRP の主要な関数コード
ms.date: 08/12/2017
ms.assetid: 11c5b1a9-74c0-47fb-8cce-a008ece9efae
ms.localizationpriority: medium
ms.openlocfilehash: 0730d2e2664bcd00e8d4c18067ccc526ae3d2746
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716926"
---
# <a name="irp-major-function-codes"></a>IRP の主要な関数コード





各ドライバー固有の I/O スタックの場所 (**IO\_スタック\_場所**主な機能がコードをサポートする必要があります。

特定の操作の実行をドライバーを指定した**IRP\_MJ\_<em>XXX</em>** コードでは、基になるデバイスにある程度を左右の特に[ **IRP\_MJ\_デバイス\_コントロール**](irp-mj-device-control.md)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)要求。 たとえば、キーボード ドライバーに送信された要求は必ずしも少し異なるディスク ドライバーに送信されたものです。 ただし、I/O マネージャーは、パラメーターと主要な関数のシステム定義の各コードの I/O スタックの場所の内容を定義します。

上位レベルのすべてのドライバーが、下位レベルの次のドライバーと呼び出しの Irp で適切なの I/O のスタックの場所を設定する必要があります[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)、各入力の IRP またはドライバーが作成した IRP のいずれか (場合、高度なドライバーを保持したまま IRP の入力)。 その結果、すべての中間ドライバーには、基になるデバイス ドライバーを処理する各メジャーの関数コードのディスパッチ ルーチンが必要です。 それ以外の場合、新しい中間ドライバー「チェーンが破壊」されるたびに、アプリケーションのまたはまだより高度なドライバーが、デバイス ドライバーを基になるまでの I/O 要求を送信しようとしています。 します。

ファイル システム ドライバーが必要なシステム定義のサブセットを処理も**IRP\_MJ\_<em>XXX</em>** 関数コード、従属要素を使用して一部**IRP\_MN\_ <em>XXX</em>** コードに機能します。

ドライバーは Irp が次の主要な機能コードの一部またはすべての設定を処理します。

[**IRP\_MJ\_クリーンアップ**](irp-mj-cleanup.md)

[**IRP\_MJ\_CLOSE**](irp-mj-close.md)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**IRP\_MJ\_DEVICE\_CONTROL**](irp-mj-device-control.md)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

[**IRP\_MJ\_フラッシュ\_バッファー**](irp-mj-flush-buffers.md)

[**IRP\_MJ\_内部\_デバイス\_コントロール**](irp-mj-internal-device-control.md)

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

[**IRP\_MJ\_電源**](irp-mj-power.md)

[**IRP\_MJ\_クエリ\_情報**](irp-mj-query-information.md)

[**IRP\_MJ\_READ**](irp-mj-read.md)

[**IRP\_MJ\_SET\_INFORMATION**](irp-mj-set-information.md)

[**IRP\_MJ\_シャット ダウン**](irp-mj-shutdown.md)

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

[**IRP\_MJ\_WRITE**](irp-mj-write.md)

このセクションで説明されているパラメーターの入力と出力のパラメーターは、IRP の関数に固有のパラメーターです。

Irp の詳細については、次を参照してください。 [Irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)します。

 

 




