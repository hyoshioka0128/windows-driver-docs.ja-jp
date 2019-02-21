---
title: ページアウトのヘッダーからの読み取りシンボル
description: ページアウトのヘッダーからの読み取りシンボル
ms.assetid: 74ec20d8-e2b5-449d-8b93-7553c57fac07
keywords:
- シンボル、ページ アウト ヘッダーの問題
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 267b6ef8d4ad4a9286e8601146cd056277cd12c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531665"
---
# <a name="reading-symbols-from-paged-out-headers"></a>ページアウトのヘッダーからの読み取りシンボル


## <span id="ddk_reading_symbols_from_paged_out_headers_dbg"></span><span id="DDK_READING_SYMBOLS_FROM_PAGED_OUT_HEADERS_DBG"></span>


カーネル デバッガーでは、そのモジュールに対応しているシンボルを確認するには読み込まれている各モジュールのイメージのヘッダーを読み取る必要があります。

モジュールのヘッダーをディスクにページアウトしている場合、デバッガーはこのモジュールのシンボルが読み込まれません。 モジュールがデバッグ プロセスに不可欠な場合は、重要な問題であることができます。

次の手順は、この問題を解決するために使用できます。

**ページアウトのヘッダーのシンボルを取得するには**

1.  カーネル自体の 2 番目のコピーを作成します。 おそらく、これをネットワーク共有に配置する最も簡単なになります。

2.  この共有のルート ディレクトリをシンボル パスに追加します。 参照してください[シンボル パス](symbol-path.md)シンボル パスを変更する方法についてはします。

3.  使用して、 [ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンド。

4.  使用して、 [ **! sym ノイズの多い**](-sym.md)拡張機能コマンドより詳細な出力を参照してください。 これを使用する場合は、どのシンボルが、対象のコンピューター上のモジュール イメージから読み込まれ、カーネル モジュールのコピーから読み込まれてを参照してくださいできなきます。

この方法は、デバッガーには、元のファイルが実際にファイルのコピーに一致するかどうかを検証する方法があるないので注意して使用する必要があります。 ネットワーク共有で使用される Windows のバージョンがターゲット コンピューターで使用されているバージョンと一致することが重要です。

この手法は、カーネル モードのデバッグにのみ使用されます。 オペレーティング システムでは、(ページング ファイルを保持するディスクは、マウント解除されたか、それ以外の場合にアクセスできない) 場合を除き、ユーザー モードのデバッグ中に必要なすべてのヘッダーにページングできます。

使用されているこの手法の例を次に示します。

```dbgcmd
kd> .reload
Connected to Windows XP 2268 x86 compatible target, ptr64 FALSE
Loading Kernel Symbols
..........Unable to read image header for dmload.sys at fe0be000 - NTSTATUS 0xC0000001
..........Unable to read image header for dmboot.sys at fda93000 - NTSTATUS 0xC0000001
.....................................Unable to read image header for fdc.sys at fdfc2000 - NTSTATUS 0xC0000001
...Unable to read image header for flpydisk.sys at fde4a000 - NTSTATUS 0xC0000001
.Unable to read image header for Fs_Rec.SYS at fe0c8000 - NTSTATUS 0xC0000001
.Unable to read image header for Null.SYS at fe2c4000 - NTSTATUS 0xC0000001
...................Unable to read image header for win32k.sys at a0000000 - NTSTATUS 0xC0000001
..Unable to read image header for dxg.sys at a0194000 - NTSTATUS 0xC0000001
.......Unable to read image header for ati2draa.dll at a01a4000 - NTSTATUS 0xC0000001
..Unable to read image header for ParVdm.SYS at fe116000 - NTSTATUS 0xC0000001
.......
Loading unloaded module list
..............
Loading User Symbols
Unable to retrieve the PEB address. This is usually caused
by being in the wrong process context or by paging
```

多くのイメージにアクセスできないヘッダーがあることに注意してください。 これらのファイルのいずれかからシンボルを確認してください (この例では、fs\_rec.sys)。

```dbgcmd
kd> x fs_rec!*
*** ERROR: Module load completed but symbols could not be loaded for fs_rec.sys
```

これらのヘッダーをページ アウトは明らかです。これは、適切なイメージをシンボル パスに追加する必要があります。

```dbgcmd
kd> .sympath+ \\myserver\myshare\symbols\x86fre\symbols
Symbol search path is: symsrv*symsrv.dll*c:\localcache*https://msdl.microsoft.com/download/symbols;\\myserver\myshare\symbols\x86fre\symbols

kd> .reload
Connected to Windows XP 2268 x86 compatible target, ptr64 FALSE
Loading Kernel Symbols
..........Unable to read image header for dmload.sys at fe0be000 - NTSTATUS 0xC0000001
..........Unable to read image header for dmboot.sys at fda93000 - NTSTATUS 0xC0000001
.....................................Unable to read image header for fdc.sys at fdfc2000 - NTSTATUS 0xC0000001
...Unable to read image header for flpydisk.sys at fde4a000 - NTSTATUS 0xC0000001
.Unable to read image header for Fs_Rec.SYS at fe0c8000 - NTSTATUS 0xC0000001
.Unable to read image header for Null.SYS at fe2c4000 - NTSTATUS 0xC0000001
...................Unable to read image header for win32k.sys at a0000000 - NTSTATUS 0xC0000001
..Unable to read image header for dxg.sys at a0194000 - NTSTATUS 0xC0000001
.......Unable to read image header for ati2draa.dll at a01a4000 - NTSTATUS 0xC0000001
..Unable to read image header for ParVdm.SYS at fe116000 - NTSTATUS 0xC0000001
.......
Loading unloaded module list
..............
Loading User Symbols
Unable to retrieve the PEB address. This is usually caused
by being in the wrong process context or by paging
```

同じ警告が表示されてが自体のシンボルがアクセスできるようになりました。

```dbgcmd
kd> x fs_Rec!*
fe0c8358  Fs_Rec!_imp___allmul
fe0c8310  Fs_Rec!_imp__IoCreateDevice
fe0c835c  Fs_Rec!_imp___allshr
........
fe0c8360  Fs_Rec!ntoskrnl_NULL_THUNK_DATA
fe0c832c  Fs_Rec!_imp__KeSetEvent
fe0c9570  Fs_Rec!_NULL_IMPORT_DESCRIPTOR
```

 

 





