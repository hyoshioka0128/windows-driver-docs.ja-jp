---
title: バッファー付き I/O とダイレクト I/O のどちらも使用しない
description: バッファー付き I/O とダイレクト I/O のどちらも使用しない
ms.assetid: e85af2e0-e532-47ca-918e-087e7aff859e
keywords:
- バッファー WDK の I/O バッファーもダイレクト I/O
- データ バッファーの WDK I/O、バッファーもダイレクト I/O
- バッファーも直接 I/O WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 775518a5a4e41faeab385d281fee24a099d04f0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381612"
---
# <a name="using-neither-buffered-nor-direct-io"></a>バッファー付き I/O とダイレクト I/O のどちらも使用しない





バッファーも直接 I/O ドライバーを使用している場合、I/O マネージャー元のユーザー スペースの仮想アドレスで渡します Irp がドライバーに送信します。 これらのバッファーを安全にアクセスするには、呼び出し元のスレッドのコンテキストで、ドライバーを実行する必要があります。 通常、そのため、fsd に対して表示されるなどの最上位レベル ドライバー メソッド使用できますこのバッファーにアクセスするため。

中級以上の最下位レベルのドライバーは、この条件を満たす常にことはできません。 たとえば、要求元のスレッドが I/O 要求の完了を待機している場合、または場合より高度なドライバー上に構築された、中級以上の最下位レベルのドライバー、下位レベルのドライバーのルーチンは、要求元のスレッドのコンテキストで呼び出される可能性がありますが。

I/O マネージャーは、I/O 操作がバッファーもダイレクト I/O を次のように使用しているかを決定します。

-   [ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)と[ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求どちらの操作を行います\_バッファーに格納された\_IO も DO\_直接\_で IO が設定されて、**フラグ**のメンバー、 [**デバイス\_オブジェクト** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)構造体。 詳細については、次を参照してください。[デバイス オブジェクトを初期化して](initializing-a-device-object.md)します。

-   [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求、IOCTL コードの値には、メソッドが含まれています。\_どちらとして、 *TransferType* IOCTL 値の値。 詳細については、次を参照してください。 [I/O 制御コードを定義する](defining-i-o-control-codes.md)します。

ドライバーでは、バッファーもダイレクト I/O を使用して、I/O 操作を指定する IRP を受信すると、次の操作する必要があります。

1.  ユーザー バッファーのアドレス範囲の有効性を確認し、確認するかどうか、適切な読み取りまたは書き込みアクセスは許可されてを使用して、 [ **ProbeForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforread)と[ **ProbeForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-probeforwrite)ルーチンをサポートします。 ユーザー スレッドは、ドライバーは、メモリへのアクセス中に、バッファーのアクセス権を変更できないように、ドライバーは、ドライバーが指定した例外ハンドラー内のバッファーのアドレス範囲へのアクセスを囲む必要があります。 プローブでは、例外が発生した場合、ドライバーはエラーを返す必要があります。 ドライバーは、I/O 要求を行ったスレッドのコンテキスト内でこれらのルーチンを呼び出す必要があります。そのためより高度なドライバーだけでは、このタスクを実行できます。

2.  次の方法のいずれかでバッファーとメモリの操作を管理します。
    -   バッファー内の I/O を使用するドライバーは、I/O マネージャーのように、独自のダブル バッファリングの操作を実行します。 詳細については、次を参照してください。[を使用してバッファー I/O](using-buffered-i-o.md)します。
    -   独自の MDLs を作成し、I/O マネージャーがダイレクト I/O を使用するドライバーに対しては、メモリ マネージャーのサポートのルーチンを呼び出すことにより、バッファーをロックダウンします。 詳細については、次を参照してください。[を使用して直接 I/O](using-direct-i-o.md)します。
    -   呼び出し元のスレッドのコンテキストで直接ユーザー バッファー上のすべての必要な操作を実行します。 場合は、ドライバーは、メモリへのアクセス中に、バッファーのアクセス権またはバッファー内のデータのいずれかをユーザー スレッドが変更、ドライバーは、ドライバーが指定した例外ハンドラー内でバッファーへのアクセスをラップする必要があります。 詳細については、次を参照してください。[例外処理](handling-exceptions.md)します。

実際には、ドライバーする必要があります IRP あたりごとに呼び出し元のスレッドのコンテキストでは、バッファー内の I/O、ダイレクト I/O、または I/O を実行するかどうか選び、ユーザー モード スレッドのコンテキストで発生した例外を処理する必要があります。 ドライバーには、独自のユーザー バッファーへのアクセス、ダブル バッファリングの操作および I/O マネージャーがドライバーに対するこれらの操作を処理できるようにすることではなく、必要に応じて、メモリ マッピングを管理する必要があります。

 

 




