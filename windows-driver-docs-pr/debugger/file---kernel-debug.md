---
title: ファイルのカーネル デバッグ
description: ファイルのカーネル デバッグ
ms.assetid: a80b3572-87a0-4a9d-9b62-67e1ca65fff4
keywords:
- ファイルのカーネル デバッグ
- ファイルのカーネル デバッグ、デバッガーの開始
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eefaac7ca95add2d332034c23d79a1c19d068ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369772"
---
# <a name="file--kernel-debug"></a>File | Kernel Debug (ファイル | カーネル デバッグ)


## <span id="ddk_file_kernel_debug_dbg"></span><span id="DDK_FILE_KERNEL_DEBUG_DBG"></span>


をクリックして**カーネル デバッグ**上、**ファイル**カーネル モードでターゲット コンピューターをデバッグするメニュー。

このコマンドは、CTRL キーを押しながら K キーを押すことと同等です。 このコマンドは、WinDbg が休止モードである場合にのみ使用できます。

### <a name="span-iddialog_boxspanspan-iddialog_boxspandialog-box"></a><span id="dialog_box"></span><span id="DIALOG_BOX"></span>ダイアログ ボックス

クリックすると**カーネル デバッグ**、**カーネル デバッグ**これらのタブとダイアログ ボックスが表示されます。

- **COM**  タブは、接続が COM ポートを使用することを示します。 **ボー レート**ボックスに、ボー レートを入力します。 **ポート**ボックスに、COM ポートの名前を入力します。 詳細については、次を参照してください。[設定を、シリアル接続を手動で](setting-up-a-null-modem-cable-connection.md)します。

  名前付きパイプ経由の仮想マシンに接続する [COM] タブを使用することもできます。 **ポート**ボックスに、入力 **\\ \\** <em>VMHost</em> **\\パイプ\\** <em>PipeName</em>します。 *VMHost*仮想マシンが実行されている物理コンピューターの名前を指定します。 仮想マシンがカーネル デバッガー自体と同じコンピューターで実行している場合は、1 つのピリオド (.) を使用して、 *VMHost*します。 詳細については、次を参照してください。[接続を設定、仮想マシンに](attaching-to-a-virtual-machine--kernel-mode-.md)します。

- **1394**  タブは、接続が 1394 を使用することを示します。 **チャネル**ボックスに、1394 チャネルの数を入力します。 Windows XP または以降のバージョン、Windows オペレーティング システムの場合、ホスト コンピューターと対象のコンピュータの両方が実行している場合にのみ、1394 デバッグはサポートされています。 詳細については、次を参照してください。[を 1394 接続を手動で設定](setting-up-a-1394-cable-connection.md)します。

- **USB**  タブでは、接続が USB 2.0 接続または USB 3.0 を使用することを示します。 **ターゲット名**ボックスに、対象のコンピュータを構成したときに作成したターゲットの名前を入力します。 詳細については、次を参照してください。[設定を、USB 2.0 接続を手動で](setting-up-a-usb-2-0-debug-cable-connection.md)と[設定を、USB 3.0 接続を手動で](setting-up-a-usb-3-0-debug-cable-connection.md)します。

- **NET**  タブは、接続がイーサネットを使用することを示します。 **ポート番号**ボックスに、対象のコンピュータを構成するときに指定したポート番号を入力します。 **キー**ボックス、自動的に生成されたキーを入力します (または作成した)、ターゲット コンピューターを構成するときにします。 詳細については、次を参照してください。[設定を、ネットワーク接続を手動で](setting-up-a-network-debugging-connection.md)します。

- **ローカル** タブでは、ローカル カーネル デバッグ WinDbg を実行することを示します。 以降では、Windows XP のみ、ローカル カーネル デバッグはサポートされています。

詳細についてはおよび他のカーネル デバッグ セッションを開始する方法については、「 [Live カーネル モード デバッグを使用して WinDbg](performing-kernel-mode-debugging-using-windbg.md)します。

 

 





