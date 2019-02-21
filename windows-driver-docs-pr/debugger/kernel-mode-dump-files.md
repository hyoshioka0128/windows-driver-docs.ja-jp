---
title: カーネル モードのダンプ ファイル
description: カーネル モードのダンプ ファイル
ms.assetid: f04dc580-0e14-41aa-88a2-e04f4406add8
keywords:
- ダンプ ファイル、カーネル モード
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38e361b55eb404124d5370632dfc416d124d612b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528199"
---
# <a name="kernel-mode-dump-files"></a>カーネル モードのダンプ ファイル


## <span id="ddk_kernel_mode_dump_files_dbg"></span><span id="DDK_KERNEL_MODE_DUMP_FILES_DBG"></span>


カーネル モードのエラーが発生したときに、Microsoft Windows の既定の動作はバグ チェックのデータにブルー スクリーンを表示するがします。

ただし、選択できるいくつかの代替動作があります。

-   カーネル デバッガー (WinDbg、KD など) に接続することができます。

-   メモリ ダンプ ファイルを書き込むことができます。

-   システムは自動的に再起動できます。

-   メモリ ダンプ ファイルを書き込むことができ、システムが後で自動的に再起動できます。

このセクションでは、作成し、カーネル モードのメモリ ダンプ ファイルを分析する方法について説明します。 クラッシュ ダンプ ファイルの 3 つの異なる種類があります。 ただし、ダンプ ファイルはこれまでれないことに便利で障害が発生したシステムに接続されているライブのカーネル デバッガーには汎用性に記憶する必要があります。

このセクションの内容:

[さまざまなカーネル モードのダンプ ファイル](varieties-of-kernel-mode-dump-files.md)

[カーネル モードのダンプ ファイルを作成します。](creating-a-kernel-mode-dump-file.md)

[カーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file.md)

 

 





