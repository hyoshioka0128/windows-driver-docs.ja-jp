---
title: アクティブ メモリ ダンプ
description: アクティブ メモリ ダンプ
ms.assetid: b40979b6-cd9a-4655-8030-8bde25d75113
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a9f9f77986e00110db1338a7d8933a9e690d0e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581130"
---
# <a name="active-memory-dump"></a>アクティブ メモリ ダンプ


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


*アクティブなメモリ ダンプ*に似ていますが、[完全メモリ ダンプ](complete-memory-dump.md)、されないが、ホスト コンピューター上の問題のトラブルシューティングに関係する可能性があるページをフィルター処理が。 このフィルター処理のために、完全メモリ ダンプよりもかなり小さいは通常します。 

このダンプ ファイルには、ユーザー モード アプリケーションに割り当てられたメモリが含まれます。 Windows のカーネルおよびハードウェア アブストラクション レイヤー (HAL) に割り当てられたメモリとカーネル モード ドライバーと他のカーネル モードのプログラムに割り当てられるメモリも含まれています。 ダンプには、スタンバイ、デバッグと、選択的に裏付けられたページファイルの遷移では、便利なカーネルまたはユーザーの領域にマップするアクティブなページが含まれていて、VirtualAlloc またはページ ファイルに割り当てられたメモリなどの変更ページ セクションをバックアップします。 無料のページおよびゼロの一覧、ファイルのキャッシュ、ゲスト VM のページおよびさまざまな種類のメモリをデバッグ中に有用である可能性が低い、アクティブなダンプを含めないでください。 

アクティブなメモリ ダンプは、Windows 仮想マシン (Vm) をホストしているときに特に便利です。 完全メモリ ダンプを作成する際は、各 VM の内容が含まれます。 実行している複数の Vm が存在する場合、ホスト システムで使用されているメモリの大量のこのアカウントのことができます。 多くの場合、関心のあるコード アクティビティは、親のホスト OS では、子 Vm ではなくします。 アクティブなメモリ ダンプは、すべての子 Vm に関連付けられているメモリが除外されます。 

アクティブなメモリ ダンプ ファイルは %systemroot% に書き込まれます\\既定 Memory.dmp します。

アクティブなメモリ ダンプは、以降 Windows 10 で利用できます。

**注**  作業中のメモリ ダンプをデバッグするときに、不足しているページのエラー メッセージを非表示に使用して、 [ **.ignore\_不足している\_ページ**](-ignore-missing-pages--suppress-missing-page-errors-.md)コマンド。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[さまざまなカーネル モードのダンプ ファイル](varieties-of-kernel-mode-dump-files.md)

 

 






