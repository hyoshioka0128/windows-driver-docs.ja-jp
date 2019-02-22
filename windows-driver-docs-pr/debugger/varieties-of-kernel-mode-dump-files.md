---
title: さまざまなカーネル モードのダンプ ファイル
description: さまざまなカーネル モードのダンプ ファイル
ms.assetid: 6db2a755-ed9c-492a-a650-9ae34ae59968
keywords:
- ダンプ ファイル、カーネル モードのファイルの種類
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f963d98be95c454f2be57cadbaaf792c09927e77
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549209"
---
# <a name="varieties-of-kernel-mode-dump-files"></a>さまざまなカーネル モードのダンプ ファイル


## <span id="ddk_varieties_of_kernel_mode_dump_files_dbg"></span><span id="DDK_VARIETIES_OF_KERNEL_MODE_DUMP_FILES_DBG"></span>


カーネル モードのクラッシュ ダンプ ファイルの 5 つの設定があります。

[完全メモリ ダンプ](complete-memory-dump.md)

[カーネル メモリ ダンプ](kernel-memory-dump.md)

[小さいメモリ ダンプ](small-memory-dump.md)

[自動メモリ ダンプ](automatic-memory-dump.md)

[アクティブなメモリ ダンプ](active-memory-dump.md)

これらのダンプ ファイルの違いは、サイズのいずれかです。 *完全メモリ ダンプ*が最大とユーザー モード メモリの一部を含む情報、最もが含まれています。 *アクティブなメモリ ダンプ*は若干小さくなりますが、ほとんどの目的で同様の情報が含まれています。  *カーネル メモリ ダンプ*はまだ小さいため、通常ユーザー モードのメモリを省略し、*最小メモリ ダンプ*は 64 KB のサイズのみ。

選択した場合*メモリ ダンプを自動*、ダンプ ファイルは、カーネル メモリ ダンプと同じですが、Windows がより柔軟にシステムのページング ファイルのサイズを設定します。

大きなファイルの利点ができる、詳細については、含まれているため、クラッシュの原因を探すのに役立つ可能性が高くなります。

小さいファイルの利点が小さくなり、書き込まれたより迅速にです。 速度が重要です。 多くの場合、サーバーを実行している場合、サーバー クラッシュの後、できるだけ早く再起動することがあり、再起動は、ダンプ ファイルが書き込まれるまで行われません。

完全メモリ ダンプまたはカーネル メモリ ダンプが作成されたら後、は、大きなダンプ ファイルから小さいメモリ ダンプ ファイルを作成することはできます。 参照してください、 [ **.dump (ダンプ ファイルの作成)** ](-dump--create-dump-file-.md)詳細コマンド。

**注**  カーネル モードのダンプ ファイルを分析することで、多くの情報を取得できます。 ただし、カーネル モードのダンプ ファイルが提供できない情報をできるだけ実際にカーネル デバッガーで直接、クラッシュをデバッグします。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネル モードのダンプ ファイル](kernel-mode-dump-files.md)

[カーネル モードのダンプ ファイルを有効にします。](enabling-a-kernel-mode-dump-file.md)

 

 






