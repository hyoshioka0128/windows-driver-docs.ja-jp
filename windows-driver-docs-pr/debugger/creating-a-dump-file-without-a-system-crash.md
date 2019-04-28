---
title: システム クラッシュなしのダンプ ファイルの作成
description: システム クラッシュなしのダンプ ファイルの作成
ms.assetid: 747194d0-0aac-487a-acdc-ff27721606d4
keywords:
- ダンプ ファイル、システムがクラッシュせずに作成
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 211b9c107050fcfdffa4204cc8f1f75cdc120003
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375476"
---
# <a name="creating-a-dump-file-without-a-system-crash"></a>システム クラッシュなしのダンプ ファイルの作成


## <span id="ddk_creating_a_dump_file_without_a_system_crash_dbg"></span><span id="DDK_CREATING_A_DUMP_FILE_WITHOUT_A_SYSTEM_CRASH_DBG"></span>


KD または WinDbg を実行するカーネル モードのデバッグ、対象のコンピュータを起こさずに書き込まれるカーネル モードのダンプ ファイルが発生します。

このダンプ ファイルには、完全メモリ ダンプまたは小さいメモリ ダンプのどちらかを指定できます。 コントロール パネルの設定では、このアクションに関係ありません。

クラッシュしているコンピューターには、システムのクラッシュの原因となったダンプ ファイルが書き込まれる、一方は、ホスト コンピューターにこのダンプ ファイルが書き込まれます。

詳細については、次を参照してください。、 [ **.dump (ダンプ ファイルの作成)** ](-dump--create-dump-file-.md)コマンド。

 

 





