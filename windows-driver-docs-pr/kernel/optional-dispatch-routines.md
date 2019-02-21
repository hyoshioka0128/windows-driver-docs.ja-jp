---
title: 省略可能なディスパッチ ルーチン
description: 省略可能なディスパッチ ルーチン
ms.assetid: 38a3fcc9-237d-432d-85db-1594697c96a5
keywords:
- ルーチンの WDK カーネルをディスパッチする、省略可能
- 省略可能なディスパッチ ルーチン WDK カーネル
- 大容量記憶装置デバイス WDK ディスパッチ ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 361e81c6ed13f342ac821baf727a4e07f30ce8a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538480"
---
# <a name="optional-dispatch-routines"></a>省略可能なディスパッチ ルーチン





ドライバーには、次のディスパッチ ルーチンが含まれます。

-   [*DispatchCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    [**IRP\_MJ\_クリーンアップ**](https://msdn.microsoft.com/library/windows/hardware/ff550718)ターゲット デバイス オブジェクトに関連付けられているファイル オブジェクトの最後のハンドルが閉じられることを示します。 ファイル オブジェクトの未処理の I/O 要求される可能性があります。 ドライバーが実装できる、 *DispatchCleanup*ルーチンは特定のファイル ハンドルのいずれかに固有のクリーンアップを実行します。 ドライバーを使用することも、 [ *DispatchClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)同じ目的で、日常的な。

-   [*DispatchQueryInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 [ *DispatchSetInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    一部の最上位レベルのドライバーがあるプロセスに[ **IRP\_MJ\_クエリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550788)と[ **IRP\_MJ\_設定\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550799) Irp します。 このような要求がユーザー モード アプリケーション、カーネル モード コンポーネント、またはドライバーがユーザー モードの要求者がハンドル、または対象のファイル オブジェクト (ドライバーのデバイス オブジェクトを表す) の長さに関する情報を要求ことを示すため、ユーザー モード要求元がそのファイルのオブジェクトで、ファイルの終わり-を設定しようとしています。

    Parallel クラスやシリアル デバイス ドライバーは、設定してこれらの要求を処理、 [**ファイル\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545855)または[ **ファイル\_位置\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545848)長さまたは 0 に位置します。 他の最上位レベルのデバイス ドライバーは、これらの要求をサポートする場合、ユーザー モード アプリケーションまたはカーネル モード ドライバーは、ファイル オブジェクトを操作する C ランタイム関数を呼び出すことができます。 ファイル システム ドライバーは、これらの要求を最上位レベルのこれらのデバイス ドライバーよりも完全にサポートする必要があります。

-   [*DispatchFlushBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    ドライバーのデバイスでデータをキャッシュまたはドライバーに割り当てられたメモリにデータを内部的にバッファーを受け取ることがあります[ **IRP\_MJ\_フラッシュ\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff550760)します。 この要求の受信は、ドライバーは、バッファー内のデータを書き込む必要があります、またはバッファー処理またはキャッシュされたデバイスから読み取られたデータをフラッシュ、キャッシュされたデータ、デバイスを out または破棄する必要がありますを示します。

    たとえば、システム キーボードとマウス クラス ドライバーを自分のデバイスからの入力データの内部リング バッファーを持ちは、フラッシュの要求をサポートします。 大容量記憶装置のドライバーとドライバーがそれらの上に配置は、この要求もサポートします。

-   [*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

    システムがシャット ダウン前に呼び出される可能性がある任意のドライバーを処理する必要があります[ **IRP\_MJ\_シャット ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff550807)します。 *DispatchShutdown*ルーチンが電源マネージャー、システムに送信する前に必要になどのドライバーにより決定されたクリーンアップを行う必要がありますセット power IRP、システムをシャット ダウンします。 ドライバーが呼び出せる[ **IoRegisterShutdownNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549541)または[ **IoRegisterLastChanceShutdownNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff549518)に登録するにはシャット ダウンの通知。

大容量記憶装置のドライバーと上層にあるそれらの中間ドライバーは、システムをシャット ダウンするときにシャット ダウンの Irp に送信するファイル システム ドライバーを最上位レベルに依存できます。 つまり、FSD 担当の周辺機器に、キャッシュされたファイルのデータを書き込むことを確認する場合、システムがシャット ダウンする前に、デバイスのキャッシュまたはバッファー (ある場合)、およびなどからのデータのフラッシュを基になるドライバーの呼び出し。

内部的にデータをキャッシュする大容量記憶装置のドライバーを提供する必要があります*DispatchShutdown*と*DispatchFlushBuffers*ルーチン。 大容量記憶装置ドライバーがメモリにデータをバッファーのデバイスには、内部キャッシュにない場合は、またする必要があります提供*DispatchShutdown*と*DispatchFlushBuffers*ルーチン。

任意の中間ドライバーが処理するドライバーの上に配置[ **IRP\_MJ\_フラッシュ\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff550760)と[ **IRP\_MJ\_シャット ダウン**](https://msdn.microsoft.com/library/windows/hardware/ff550807)要求も提供*DispatchShutdown*と*DispatchFlushBuffers*ルーチン。

 

 




