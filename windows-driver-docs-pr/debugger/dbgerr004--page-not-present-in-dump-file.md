---
title: dbgerr004 ページのダンプ ファイルに存在しません。
description: dbgerr004 ページのダンプ ファイルに存在しません。
ms.assetid: e76d11fc-857b-4a40-8f41-f34f3bcade57
keywords:
- dbgerr004
- ページのダンプ ファイル (dbgerr004) 内にありません。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91602c01f37f74844e263b7457f29b8aff6e442c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374386"
---
# <a name="dbgerr004-page-not-present-in-dump-file"></a>dbgerr004:Page Not Present in Dump File


## <span id="ddk_dbgerr004_dbg"></span><span id="DDK_DBGERR004_DBG"></span>


デバッガーのエラー **dbgerr004** 、メッセージが表示されます"ページ*数*ダンプ ファイルに存在しません"。 このエラーは、デバッガーがデバッグ ダンプ ファイルに含まれていないメモリ ページが必要であることを示します。

指定した*数*は元のページの物理メモリ内の場所に対応するページのフレーム数 (PFN) です。

このエラー メッセージを抑制するのには、使用、 [ **.ignore\_不足している\_ページ 1** ](-ignore-missing-pages--suppress-missing-page-errors-.md)コマンド。 このコマンドは、デバッグを続行することができますが、このエラー メッセージは表示されません。

カーネル モードのメモリ ダンプには 3 つのサイズと、比較的小さなサイズでは、すべてのメモリ ページは含まれません。 詳細については、次を参照してください。[さまざまなカーネル モードのダンプ ファイルの](varieties-of-kernel-mode-dump-files.md)します。

ユーザー モードのメモリ ダンプは、さまざまなサイズにも付属します。 参照してください[ユーザー モード ダンプ ファイル](user-mode-dump-files.md)詳細についてはします。

 

 





