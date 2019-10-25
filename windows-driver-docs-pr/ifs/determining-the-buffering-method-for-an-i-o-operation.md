---
title: I/O 操作用のバッファー処理メソッドの確認
description: I/O 操作用のバッファー処理メソッドの確認
ms.assetid: 219378d9-a9fa-495a-b016-36595a7efb49
keywords:
- WDK ファイルシステムミニフィルターのバッファー
- preoperation コールバックルーチン WDK ファイルシステムミニフィルター、バッファー
- postoperation コールバックルーチン WDK ファイルシステムミニフィルター、バッファー
- バッファーされた i/o WDK ファイルシステム
- ダイレクト i/o WDK ファイルシステム
- バッファーも直接 i/o WDK ファイルシステムもありません
- データバッファー WDK ファイルシステムミニフィルター
- I/o WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb544b5f22bd583ec458fddd24ecd0744d83f05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841439"
---
# <a name="determining-the-buffering-method-for-an-io-operation"></a>I/O 操作用のバッファー処理メソッドの確認


## <span id="ddk_determining_the_buffering_method_for_an_io_operation_if"></span><span id="DDK_DETERMINING_THE_BUFFERING_METHOD_FOR_AN_IO_OPERATION_IF"></span>


デバイスドライバーと同様に、ファイルシステムはユーザーモードアプリケーションとシステムデバイス間でデータを転送します。 オペレーティングシステムには、データバッファーにアクセスするための次の3つの方法が用意されています。

-   *バッファー*内 i/o では、i/o マネージャーは、非ページプールから操作用のシステムバッファーを割り当てます。 I/o マネージャーは、i/o 操作を開始したスレッドのコンテキストで、このシステムバッファーからアプリケーションのユーザーバッファーにデータをコピーします。その逆も同様です。

-   *ダイレクト i/o*では、i/o マネージャーによってユーザーバッファーがプローブおよびロックされます。 次に、ロックされたバッファーをマップするためのメモリ記述子リスト (MDL) を作成します。 I/o マネージャーは、i/o 操作を開始したスレッドのコンテキストでバッファーにアクセスします。

-   *バッファーも直接*i/o でも、i/o マネージャーはシステムバッファーを割り当てません。また、ユーザーバッファーをロックまたはマップしません。 代わりに、単にバッファーの元のユーザー領域の仮想アドレスをファイルシステムスタックに渡します。 ドライバーは、それらが開始スレッドのコンテキストで実行されていること、およびバッファーアドレスが有効であることを確認する役割を担います。

    ミニフィルタードライバーを使用する前に、ユーザー領域内のアドレスを検証する必要があります。 I/o マネージャーとフィルターマネージャーでは、このようなアドレスは検証されず、ミニフィルタードライバーに渡されたバッファーに埋め込まれているポインターは検証されません。

すべての標準の Microsoft ファイルシステムでは、ほとんどの i/o 処理で、バッファーも直接 i/o も使用されません。

バッファリングメソッドの詳細については、「[データバッファーにアクセスするためのメソッド](https://docs.microsoft.com/windows-hardware/drivers/kernel/methods-for-accessing-data-buffers)」を参照してください。

IRP ベースの i/o 操作の場合、使用されるバッファリング方法は操作に固有であり、次の要因によって決定されます。

-   実行されている i/o 操作の種類

-   ファイルシステムボリュームの[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の**Flags**メンバーの値

-   I/o 制御 (IOCTL) 操作とファイルシステム制御 (FSCTL) 操作の場合、IOCTL または FSCTL が定義されたときに CTL\_コードマクロに渡された*Transfertype*パラメーターの値

バッファーを持つ高速 i/o 操作では、バッファーも直接も直接使用されません。

ファイルシステムコールバック操作にはバッファーがありません。

このセクションの内容:

[IRP ベースまたは高速 i/o の可能性がある操作](operations-that-can-be-irp-based-or-fast-i-o.md)

[デバイスオブジェクトフラグに従う IRP ベースの i/o 操作](irp-based-i-o-operations-that-obey-device-object-flags.md)

[バッファリングされた i/o を常に使用する IRP ベースの i/o 操作](irp-based-i-o-operations-that-always-use-buffered-i-o.md)

[常にバッファーも直接も直接使用する IRP ベース i/o 操作](irp-based-i-o-operations-that-always-use-neither-buffered-nor-direct-i.md)

[IRP ベースの IOCTL および FSCTL 操作](irp-based-ioctl-and-fsctl-operations.md)

[バッファーを持たない IRP ベースの i/o 操作](irp-based-i-o-operations-that-have-no-buffers.md)

 

 




