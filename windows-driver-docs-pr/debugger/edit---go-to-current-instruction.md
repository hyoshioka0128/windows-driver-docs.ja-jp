---
title: 現在の命令に移動を編集します。
description: 現在の命令に移動を編集します。
ms.assetid: 7bc57ac1-1de6-4534-836b-132e3b072ae5
keywords:
- 現在の命令に移動を編集します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b81ca7013fb3506972a1fd8956dd0fc4badcb49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331401"
---
# <a name="edit--go-to-current-instruction"></a>Edit | Go to Current Instruction (編集 | 現在の命令に移動)


## <span id="ddk_edit_go_to_current_instruction_dbg"></span><span id="DDK_EDIT_GO_TO_CURRENT_INSTRUCTION_DBG"></span>


をクリックして**現在の命令に移動**上、**編集** メニューの 現在の命令を含むデバッグ情報 ウィンドウを開くと、この命令を強調表示します。

このコマンドは、ALT + アスタリスク (テンキーのアスタリスク キーを使用) を押すことと同等です。

現在の命令に対応する既知のソース ファイル、WinDbg 開きます、[ソース ウィンドウ](source-window.md)このソース ファイルを格納しています。 このようなウィンドウが存在しない場合 WinDbg では、いずれかが表示されます。 現在の行が強調表示されます。

現在の命令が既知のソース ファイルでないかどうか、[逆アセンブル ウィンドウ](disassembly-window.md)は開くには、逆アセンブル ウィンドウと現在の行が強調表示されている WinDbg が開きます。 ただし、逆アセンブル ウィンドウが閉じている場合、**現在の命令に移動**コマンドは開いていません。

このコマンドでは、WinDbg 表示が変わるだけです。 このコマンドは、ターゲットまたは他のデバッガー操作の実行には影響しません。

 

 





