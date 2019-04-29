---
title: カーネルモード ダンプ ファイルの検証と作成
description: カーネルモード ダンプ ファイルの検証と作成
ms.assetid: ea1dc18d-8974-4de8-accd-1cbc515d71d0
keywords:
- ダンプ ファイル、カーネル モード ダンプの作成を確認しています
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a372db165443b67b14a3e88722fd389a9968b551
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386435"
---
# <a name="verifying-the-creation-of-a-kernel-mode-dump-file"></a>カーネルモード ダンプ ファイルの検証と作成


## <span id="ddk_verifying_the_creation_of_a_kernel_mode_dump_file_dbg"></span><span id="DDK_VERIFYING_THE_CREATION_OF_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


デバッガーに分割するマシンがある場合は、不明なクラッシュ ダンプ ファイルが正常に書き込まれるかどうかは、次のコマンドを実行します。

```dbgcmd
dd nt!IopFinalCrashDumpStatus L1
```

値が表示されます、 **IopFinalCrashDumpStatus**変数。

この値が 0 の場合、プロセスが成功します。 -1 (0 xffffffff) の場合、ダンプ プロセスが開始されません。

その他の値は、ダンプ プロセス中にエラーを示すステータス コードです。

 

 





