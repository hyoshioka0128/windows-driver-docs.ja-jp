---
title: I/O 操作用のバッファー処理メソッドの確認
description: I/O 操作用のバッファー処理メソッドの確認
ms.assetid: 219378d9-a9fa-495a-b016-36595a7efb49
keywords:
- バッファー WDK ファイル システム ミニフィルター
- preoperation コールバック ルーチン WDK ファイル システム ミニフィルター、バッファー
- postoperation コールバック ルーチン WDK ファイル システム ミニフィルター、バッファー
- バッファー内の I/O の WDK ファイル システム
- ダイレクト I/O WDK ファイル システム
- バッファーも直接 I/O WDK のファイル システム
- データ バッファーの WDK ファイル システム ミニフィルター
- ファイル システムの I/O の WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f21cc89dd5d464b6d993178b70342571b1f2707f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578633"
---
# <a name="determining-the-buffering-method-for-an-io-operation"></a>I/O 操作用のバッファー処理メソッドの確認


## <span id="ddk_determining_the_buffering_method_for_an_io_operation_if"></span><span id="DDK_DETERMINING_THE_BUFFERING_METHOD_FOR_AN_IO_OPERATION_IF"></span>


デバイス ドライバーのようなファイル システムはユーザー モード アプリケーションとシステムのデバイス間でデータを転送する責任を負います。 オペレーティング システムでは、データ バッファーにアクセスするため次の 3 つのメソッドを提供します。

-   *I/O バッファー*、I/O マネージャーは非ページ プールから、操作をシステムのバッファーを割り当てます。 I/O マネージャーは、アプリケーションのユーザーのバッファーに、その逆の場合、I/O 操作を開始したスレッドのコンテキストで、このシステムのバッファーからデータをコピーします。

-   *ダイレクト I/O*、I/O マネージャーがプローブし、ユーザーのバッファーをロックします。 メモリの記述子のリストにロックされているバッファーをマップするには、(MDL) が作成されます。 I/O マネージャーでは、I/O 操作を開始したスレッドのコンテキスト内のバッファーにアクセスします。

-   *バッファーも直接 I/O*、I/O マネージャーは、システムの割り当てバッファーしはしないロックまたはユーザー バッファーをマップします。 代わりに、ファイル システムのスタックにその、単に、バッファーの元のユーザー スペースの仮想アドレスを渡します。 ドライバーは、発信側のスレッドのコンテキストで実行されていることと、バッファーのアドレスが有効であることを確認します。

    ミニフィルター ドライバーは、これを使用する前にユーザー領域で任意のアドレスを検証する必要があります。 I/O マネージャーとフィルター マネージャーは、このようなアドレスを検証しないとミニフィルター ドライバーに渡されるバッファーに埋め込まれているポインターを検証できません。

すべての標準的な Microsoft ファイル システムでは、ほとんどの I/O 処理バッファーもダイレクト I/O を使用します。

バッファリング メソッドの詳細については、[メソッドにアクセスするデータ バッファーの](https://msdn.microsoft.com/library/windows/hardware/ff554436)を参照してください。

IRP ベースの I/O 操作では、バッファリングに使用されるメソッドは操作固有でありは、次の要因によって決まります。

-   実行されている I/O 操作の種類

-   値、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)ファイル システム ボリュームの構造

-   I/O 制御 (IOCTL) とファイル システム コントロール (FSCTL) 操作の値、 *TransferType* CTL に渡されたパラメーター\_IOCTL または FSCTL が定義されている場合、コードのマクロ

常にバッファーを持つ高速の I/O 操作では、どちらもバッファーを使用しても、ダイレクト I/O。

ファイル システムのコールバック操作では、バッファーはありません。

このセクションの内容:

[IRP ベースまたは高速の I/O をできる演算です。](operations-that-can-be-irp-based-or-fast-i-o.md)

[デバイス オブジェクトのフラグに従う IRP ベースの I/O 操作](irp-based-i-o-operations-that-obey-device-object-flags.md)

[バッファー内の I/O を使用して、常に IRP ベースの I/O 操作](irp-based-i-o-operations-that-always-use-buffered-i-o.md)

[IRP ベースの I/O 操作は常にバッファーもダイレクト I/O を使用します。](irp-based-i-o-operations-that-always-use-neither-buffered-nor-direct-i.md)

[IRP ベース IOCTL と FSCTL 操作](irp-based-ioctl-and-fsctl-operations.md)

[バッファーがない IRP ベースの I/O 操作](irp-based-i-o-operations-that-have-no-buffers.md)

 

 




