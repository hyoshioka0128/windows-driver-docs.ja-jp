---
title: ユーザー領域メモリへのアクセス
description: ユーザー領域メモリへのアクセス
ms.assetid: db0b6ba2-4cec-46c1-b13f-aba4c10a2d8c
keywords:
- メモリ管理 (WDK カーネル)、ユーザー領域メモリ
- ユーザー空間メモリ WDK カーネル
- 仮想ユーザー空間メモリ WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ca871e8892c74b4b5d9be71828c85bce0efee54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837293"
---
# <a name="accessing-user-space-memory"></a>ユーザー領域メモリへのアクセス





ドライバーは、ドライバーの現在の i/o 操作の原因となったユーザーモードスレッドのコンテキストで実行されていて、そのスレッドの仮想アドレスを使用している場合を除いて、ユーザーモードの仮想アドレスを通じてメモリに直接アクセスすることはできません。

FSDs などの最上位レベルのドライバーのみが、そのようなユーザーモードスレッドのコンテキストでディスパッチルーチンが呼び出されるようにすることができます。 最上位レベルのドライバーは、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を呼び出してユーザーバッファーをロックダウンしてから、下位のドライバー用に IRP を設定できます。

バッファー内の[i/o](methods-for-accessing-data-buffers.md)または[ダイレクト i/o](methods-for-accessing-data-buffers.md)用にデバイスオブジェクトを設定する最下位のドライバーと中間ドライバーは、i/o マネージャーまたは最上位レベルのドライバーを使用して、ロックダウンされたユーザーバッファーまたは irp 内のシステム領域バッファーに有効なアクセスを渡すことができます。

 

 




