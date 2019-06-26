---
title: ユーザー領域メモリへのアクセス
description: ユーザー領域メモリへのアクセス
ms.assetid: db0b6ba2-4cec-46c1-b13f-aba4c10a2d8c
keywords:
- メモリ管理の WDK カーネル、ユーザー スペースのメモリ
- ユーザー スペース メモリ WDK カーネル
- ユーザー スペースの仮想メモリの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2706374d83158d506457b768d0c452dcd34f44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363455"
---
# <a name="accessing-user-space-memory"></a>ユーザー領域メモリへのアクセス





ドライバーがドライバーの現在の I/O 操作の原因となったユーザー モード スレッドのコンテキストで実行されていると、そのスレッドの仮想アドレスを使用している場合を除き、メモリをユーザー モード仮想アドレスを使用アクセス直接ことはできません。

Fsd に対して表示されるなどの最上位レベル ドライバーは、ディスパッチ ルーチンが、このようなユーザー モード スレッドのコンテキストで呼び出されることを確認できます。 最上位レベルのドライバーが呼び出せる[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)低いドライバーは IRP をセットアップする前にユーザー バッファーをロックダウンします。

そのデバイス オブジェクトを設定する最下位レベルおよび中間ドライバー [I/O バッファー](methods-for-accessing-data-buffers.md)または[ダイレクト I/O](methods-for-accessing-data-buffers.md)ロックされたユーザーに有効なアクセスを渡すには、I/O マネージャーや最上位レベルのドライバーに依存できますバッファーまたはバッファーの Irp でシステムの領域にします。

 

 




