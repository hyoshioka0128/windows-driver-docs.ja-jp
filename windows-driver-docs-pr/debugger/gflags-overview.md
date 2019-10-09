---
title: GFlags の概要
description: GFlags の概要
ms.assetid: fa5c48bf-c0d0-4010-a101-381c692082bf
keywords:
- GFlags, 概要
ms.date: 06/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 98d4e6f4ccc04420e4d9053445af6bd7d5cd2a54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370838"
---
# <a name="gflags-overview"></a>GFlags の概要


## <span id="ddk_gflags_overview_dtools"></span><span id="DDK_GFLAGS_OVERVIEW_DTOOLS"></span>


GFlags (gflags.exe)、グローバル フラグ エディターは内部システムの高度な診断とトラブルシューティング機能を無効にできです。 コマンド プロンプト ウィンドウから GFlags を実行したり、そのグラフィカル ユーザー インターフェイス ダイアログ ボックスを使用します。

Gflags.exe を探してインストールする方法については、次を参照してください。 [GFlags](gflags.md)します。


次の機能をアクティブ化するのにには、GFlags を使用します。

<span id="Registry"></span><span id="registry"></span><span id="REGISTRY"></span>レジストリ  
コンピューターで実行されているすべてのプロセスのデバッグ機能をシステム全体を設定します。 これらの設定が格納されている、 **GlobalFlag**レジストリ エントリ (**HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Session Manager\\GlobalFlag**)。 Windows を再起動して、それらを変更してもう一度再起動するまでの有効なままと有効になりますがします。

<span id="Kernel_flag_settings"></span><span id="kernel_flag_settings"></span><span id="KERNEL_FLAG_SETTINGS"></span>カーネル フラグの設定  
このセッションのデバッグ機能を設定します。 これらの設定が、すぐに有効が、Windows のシャット ダウン時に失われます。 設定では、このコマンドが完了した後に開始されたすべてのプロセスに影響します。

<span id="Image_file_settings"></span><span id="image_file_settings"></span><span id="IMAGE_FILE_SETTINGS"></span>イメージ ファイルの設定  
デバッグ、特定のプログラムの機能を設定します。 これらの設定は、各プログラムの GlobalFlag レジストリ エントリに格納されます (**HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\ Windows NT\\ CurrentVersion\\  Image File Execution Options\\ *ImageFileName* \\ GlobalFlag**)。 有効になりますが、プログラムを再起動して変更するまで有効な場合。

<span id="Debugger"></span><span id="debugger"></span><span id="DEBUGGER"></span>デバッガー  
特定のプログラムがデバッガーで常に実行を指定します。 この設定は、レジストリに格納されます。 すぐに有効と、変更するまで有効なままになります。 (この機能でのみ使用できます、**グローバル フラグ** ダイアログ ボックス)。

<span id="Launch"></span><span id="launch"></span><span id="LAUNCH"></span>起動  
指定したデバッグ設定でプログラムを実行します。 デバッグ機能の設定は、プログラムが停止されるまで有効です。 (この機能はからのみ使用可能な**グローバル フラグ** ダイアログ ボックス)。

<span id="Special_Pool"></span><span id="special_pool"></span><span id="SPECIAL_POOL"></span>特別なプール  
特別なプールから、指定されたプール タグを持つ、または指定したサイズの割り当てが入力されてを要求します。 この機能を検出し、割り当てられたメモリ領域を超える書き込みや、既に解放されたメモリを参照するなど、カーネル プールの使用エラーの原因を特定できます。

以降 Windows Vista では、することができますを有効にする、無効化、および特別なプール機能を構成する (**カーネル特別なプール タグ**) 再起動を必要としない、カーネル フラグを設定またはレジストリ設定として、再起動する必要があります。

<span id="Page_heap_verification"></span><span id="page_heap_verification"></span><span id="PAGE_HEAP_VERIFICATION"></span>ヒープのページ検証  
有効にする、無効化、およびプログラムのページ ヒープの検証を構成します。 有効な場合、ページ ヒープは動的ヒープ メモリの割り当てや無料の操作などの操作を監視し、ヒープ エラーが検出されたときにデバッガー中断が発生します。

<span id="Silent_process_exit"></span><span id="silent_process_exit"></span><span id="SILENT_PROCESS_EXIT"></span>サイレント プロセスの終了  
有効にする、無効化、およびサイレント終了、プロセスの監視およびレポートを構成します。 プロセスの終了をサイレント モードでは、通知、イベント ログ、およびダンプ ファイルの作成を含む場合に発生するアクションを指定できます。 詳細については、次を参照してください。[サイレント プロセス終了時の監視](registry-entries-for-silent-process-exit.md)します。

 

 





