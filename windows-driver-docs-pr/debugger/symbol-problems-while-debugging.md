---
title: デバッグ中のシンボルに関する問題
description: デバッグ中のシンボルに関する問題
ms.assetid: 2713c371-9683-4d0d-a8ab-8a4c897ba0ab
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc7b959d45d576368aa37c4d6d3dfef6db3714a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335490"
---
# <a name="symbol-problems-while-debugging"></a>デバッグ中のシンボルに関する問題


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


無効または不足しているシンボルは、デバッガーの問題の最も一般的な原因の 1 つです。 何らかの問題を確認したら、シンボルの問題があるかどうかを確認する必要があります。

場合によっては、ソリューションでは、適切なシンボル ファイルを取得する必要があります。 それ以外の場合は、単に、シンボル ファイルが既にあるを認識するデバッガーを再構成する必要があります。 ただし、適切なシンボル ファイルが取得されない場合は、この問題を回避しより限定的な方法でターゲットをデバッグする必要があります。

このセクションの内容:

[シンボルを確認します。](verifying-symbols.md)

[シンボル名を照合します。](matching-symbol-names.md)

[ページアウトのヘッダーからの読み取りシンボル](reading-symbols-from-paged-out-headers.md)

[ページ アウトは、シンボルと、PEB のマッピング](mapping-symbols-when-the-peb-is-paged-out.md)

[シンボルのないユーザー モード プロセスのデバッグ](debugging-user-mode-processes-without-symbols.md)

[パフォーマンスが最適化されたコードのデバッグ](debugging-performance-optimized-code.md)

 

 





