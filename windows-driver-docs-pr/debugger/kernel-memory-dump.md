---
title: カーネル メモリ ダンプ
description: カーネル メモリ ダンプ
ms.assetid: 466f5b92-c9bd-4050-9ef8-469979ba0cbe
keywords:
- ダンプ ファイル、カーネル メモリ ダンプ
- カーネル メモリ ダンプ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795d9129c45bdc39254e0a22a3cd3103fd4b8261
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367194"
---
# <a name="kernel-memory-dump"></a>カーネル メモリ ダンプ


## <span id="ddk_kernel_memory_dump_dbg"></span><span id="DDK_KERNEL_MEMORY_DUMP_DBG"></span>


A*カーネル メモリ ダンプ*クラッシュの時点で、カーネルで使用中のすべてのメモリが含まれています。

この種のダンプ ファイルは、完全メモリ ダンプよりも大幅に小さくします。 通常、ダンプ ファイルは、システム上の物理メモリのサイズの約 3 分の 1 になります。 この量は、状況によって大きく異なります。

このダンプ ファイルは、割り当てられていないメモリ、またはユーザー モード アプリケーションに割り当てられたメモリは含まれません。 Windows のカーネルおよびハードウェア アブストラクション レイヤー (HAL) に割り当てられたメモリとカーネル モード ドライバーと他のカーネル モードのプログラムに割り当てられたメモリのみが含まれます。

ほとんどの場合、このクラッシュ ダンプは、最も役に立つします。 完了のメモリのダンプよりもかなり小さいですが、そののみ、クラッシュに関係することがあったと考えられるメモリ部分が除外されています。

この種ダンプ ファイルにはに、クラッシュ時にメモリ内に存在するユーザー モード実行可能ファイルのイメージが含まれていないために重要になるこの実行可能ファイルがわかった場合、実行可能イメージのパスを設定する必要もあります。

メモリ ダンプ ファイルは %systemroot% に書き込まれます\\既定 Memory.dmp します。

2 番目のバグ チェックが発生し、別のカーネル メモリ ダンプ (または完全メモリ ダンプ) が作成される、以前のファイルが上書きされます。

カーネル メモリ ダンプをデバッグするときに、不足しているページのエラー メッセージを非表示に使用して、 [ **.ignore\_不足している\_ページ**](-ignore-missing-pages--suppress-missing-page-errors-.md)コマンド。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[さまざまなカーネル モードのダンプ ファイル](varieties-of-kernel-mode-dump-files.md)

 

 






