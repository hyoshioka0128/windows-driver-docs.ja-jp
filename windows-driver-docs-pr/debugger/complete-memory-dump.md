---
title: 詳細なメモリ ダンプ
description: 詳細なメモリ ダンプ
ms.assetid: ccc4d22a-89af-4c7d-a982-f77c682cd001
keywords:
- ダンプファイル、完全なメモリダンプ
- 詳細なメモリ ダンプ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fab36095a663f955fe30bfbe92d9a17c7760452c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837822"
---
# <a name="complete-memory-dump"></a>詳細なメモリ ダンプ


## <span id="ddk_complete_memory_dump_dbg"></span><span id="DDK_COMPLETE_MEMORY_DUMP_DBG"></span>


*完全なメモリダンプ*は、最大のカーネルモードダンプファイルです。 このファイルには、Windows によって使用されるすべての物理メモリが含まれています。 既定では、完全なメモリダンプには、プラットフォームファームウェアによって使用される物理メモリが含まれません。

Windows 8 以降では、メモリダンプ全体の実行中に呼び出される、[*バグチェッカーのコールバック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)ルーチンを登録できます。 この*デバッグルーチンで*は、ドライバー固有のデータを指定してダンプファイルに追加することができます。 たとえば、この追加データには、仮想メモリ内のシステムアドレス範囲にマップされていないが、ドライバーのデバッグに役立つ情報が含まれている物理ページを含めることができます。 *バグチェック Addpages コールバック*ルーチンは、マップされていないか、仮想メモリ内のユーザーモードアドレスにマップされているドライバー所有の物理ページをダンプファイルに追加することがあります。

このダンプファイルを使用するには、ブートドライブに、少なくともメインのシステムメモリと同じサイズのページファイルが必要です。サイズが RAM 全体に 1 mb を加えたファイルを保持できる必要があります。

既定では、メモリダンプファイル全体が% SystemRoot%\\memory.dmp に書き込まれます。

2番目のバグチェックが発生し、別の完全なメモリダンプ (またはカーネルメモリダンプ) が作成された場合は、以前のファイルが上書きされます。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[カーネルモードダンプファイルの種類](varieties-of-kernel-mode-dump-files.md)

 

 






