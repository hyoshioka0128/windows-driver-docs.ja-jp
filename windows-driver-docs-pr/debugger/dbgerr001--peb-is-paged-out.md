---
title: dbgerr001 PEB がページ アウトには
description: dbgerr001 PEB がページ アウトには
ms.assetid: 60b20242-e458-4c36-b78d-17703c02b8b9
keywords:
- dbgerr001
- PEB のページ (dbgerr001) アウト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a81e0e2a6b8f2b4cf5892e88f989df9aa7527c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374934"
---
# <a name="dbgerr001-peb-is-paged-out"></a>dbgerr001:PEB is Paged Out


## <span id="ddk_dbgerr001_dbg"></span><span id="DDK_DBGERR001_DBG"></span>


デバッガーのエラー **dbgerr001** 「PEB がページ アウトします」メッセージが表示されます。 このエラーは、プロセスの環境ブロック (PEB) がアクセスできないことを示します。

シンボルを読み込むには、デバッガーは、オペレーティング システムによって読み込まれたモジュールの一覧を検索します。 ユーザー モードのモジュールの一覧へのポインターでは、PEB に格納された項目の 1 つです。

メモリを再利用するために、メモリ マネージャーはユーザー モードのデータ領域の他のプロセスまたはカーネル モードのコンポーネントをページアウト可能性があります。

このエラーが発生したときに、デバッガーで、このプロセスの PEB データ構造が読み取り可能でなくなったことが検出されたことを意味します。 最も可能性の高いがディスクにページ アウトされています。

このデータ構造がなければ、デバッガーは、どのようなイメージのシンボルを読み込む必要がありますを判断できません。

**注**  ユーザー モードのモジュールのシンボル ファイルのみに影響します。 カーネル モードのモジュールとシンボルは影響しません、ように別のリストで追跡されます。

 

 

 





