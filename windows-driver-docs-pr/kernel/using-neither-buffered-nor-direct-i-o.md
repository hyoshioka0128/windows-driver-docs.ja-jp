---
title: バッファー付き I/O とダイレクト I/O のどちらも使用しない
description: バッファー付き I/O とダイレクト I/O のどちらも使用しない
ms.assetid: e85af2e0-e532-47ca-918e-087e7aff859e
keywords:
- WDK i/o をバッファーします。バッファーも直接 i/o もありません。
- データバッファー WDK i/o (バッファーも直接 i/o もありません)
- バッファーも直接 i/o もない WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5a962faa7b874494e9c54b4d562ef8b029ca10f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838351"
---
# <a name="using-neither-buffered-nor-direct-io"></a>バッファー付き I/O とダイレクト I/O のどちらも使用しない





ドライバーがバッファーも直接 i/o も使用していない場合、i/o マネージャーは、ドライバーに送信される Irp 内の元のユーザー領域の仮想アドレスを渡します。 これらのバッファーに安全にアクセスするには、呼び出し元のスレッドのコンテキストでドライバーが実行されている必要があります。 そのため、通常は、FSDs などの最上位レベルのドライバーのみが、このメソッドを使用してバッファーにアクセスできます。

中間または最下位レベルのドライバーは、常にこの条件を満たすことはできません。 たとえば、要求元のスレッドが i/o 要求の完了を待機している場合、または上位レベルのドライバーが中間レベルまたは最下位のドライバーを中心としている場合、下位レベルのドライバーのルーチンは、要求元のスレッドのコンテキストでは呼び出されない可能性があります。

I/o マネージャーは、次のように、i/o 操作がバッファリングされていないか、または直接 i/o を使用していると判断します。

-   [**Irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求では、バッファー\_i/o も\_直接\_io も、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**Flags**メンバーで設定されません。\_ 詳細については、「[デバイスオブジェクトの初期化](initializing-a-device-object.md)」を参照してください。

-   [**Irp\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)と[**irp\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求の場合、IOCTL コードの値には*transfertype*値としてのメソッド\_含まれません。IOCTL 値。 詳細については、「 [I/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

ドライバーが、バッファリングされていない i/o 操作を指定する IRP を受信した場合は、次の操作を行う必要があります。

1.  ユーザーバッファーのアドレス範囲が有効であることを確認し、 [**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)および[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)サポートルーチンを使用して、適切な読み取りまたは書き込みアクセスが許可されているかどうかを確認します。 ドライバーが提供する例外ハンドラー内で、バッファーのアドレス範囲へのアクセスを囲む必要があります。これにより、ドライバーがメモリにアクセスしている間に、ユーザースレッドがバッファーのアクセス権を変更できなくなります。 プローブが例外を発生させた場合、ドライバーはエラーを返します。 ドライバーは、i/o 要求を行ったスレッドのコンテキスト内でこれらのルーチンを呼び出す必要があります。そのため、このタスクを実行できるのは、上位レベルのドライバーだけです。

2.  バッファーとメモリ操作は、次のいずれかの方法で管理します。
    -   I/o マネージャーがバッファー i/o を使用するドライバーに対して実行するので、独自のダブルバッファリング操作を実行します。 詳細については、「[バッファー i/o の使用](using-buffered-i-o.md)」を参照してください。
    -   I/o マネージャーが直接 i/o を使用するドライバーに対して行うように、メモリマネージャーのサポートルーチンを呼び出すことによって、独自の MDLs を作成し、バッファーをロックダウンします。 詳細については、「 [Direct i/o の使用](using-direct-i-o.md)」を参照してください。
    -   ユーザーバッファーに対して必要なすべての操作を、呼び出し元のスレッドのコンテキストで直接実行します。 ドライバーが提供する例外ハンドラー内でバッファーへのアクセスをラップする必要があります。これは、ユーザースレッドが、ドライバーがメモリにアクセスしている間にバッファーのアクセス権またはバッファー内のデータを変更した場合に発生します。 詳細については、「[例外の処理](handling-exceptions.md)」を参照してください。

実際には、ドライバーは、バッファー i/o、ダイレクト i/o、または i/o を呼び出し元スレッドのコンテキストで実行するかどうかを、IRP ごとに選択する必要があり、ユーザーモードスレッドコンテキストで発生する可能性のある例外を処理する必要があります。 ドライバーは、i/o マネージャーがドライバーの操作を処理するのではなく、独自のユーザーバッファーアクセス、ダブルバッファリング操作、およびメモリマッピングを必要に応じて管理する必要があります。

 

 




