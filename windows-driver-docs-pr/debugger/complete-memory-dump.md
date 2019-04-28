---
title: 詳細なメモリ ダンプ
description: 詳細なメモリ ダンプ
ms.assetid: ccc4d22a-89af-4c7d-a982-f77c682cd001
keywords:
- 完全メモリ ダンプ、ダンプ ファイル
- 詳細なメモリ ダンプ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab8af3de383a4830d162bb0368b22392cced4c79
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375072"
---
# <a name="complete-memory-dump"></a>詳細なメモリ ダンプ


## <span id="ddk_complete_memory_dump_dbg"></span><span id="DDK_COMPLETE_MEMORY_DUMP_DBG"></span>


A*完全メモリ ダンプ*が最大のカーネル モードのダンプ ファイル。 このファイルには、すべての Windows で使用される物理メモリが含まれます。 完全メモリ ダンプは、既定では、含まれません、プラットフォーム ファームウェアによって使用される物理メモリ。

登録する Windows 8 以降、 [ *BugCheckAddPagesCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540669)完全メモリ ダンプの中に呼び出されるルーチン。 *BugCheckAddPagesCallback*ルーチンは、ダンプ ファイルに追加するドライバー固有のデータを指定できます。 たとえば、この追加のデータは、仮想メモリ内のシステム アドレスの範囲にマップされるされませんが、ドライバーをデバッグするのに役立つ情報を格納する物理ページを含めることができます。 *BugCheckAddPagesCallback*ルーチン ダンプ ファイルに、ドライバーが所有している物理ページがマップされていないか、ユーザー モード仮想メモリ アドレスにマップされるとの追加の可能性があります。

このダンプ ファイルには、システムの主要なメモリとしてサイズ以上である、ブート ドライブ上のページファイルが必要です。全体の RAM とを組み合わせた 1 つのメガバイト数と同じサイズのファイルを保持できる必要があります。

完全メモリ ダンプ ファイルは %systemroot% に書き込まれます\\既定 Memory.dmp します。

2 番目のバグ チェックが発生し、もう 1 つ完全メモリ ダンプ (メモリ ダンプ) が作成された、前のファイルが上書きされます。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[さまざまなカーネル モードのダンプ ファイル](varieties-of-kernel-mode-dump-files.md)

 

 






