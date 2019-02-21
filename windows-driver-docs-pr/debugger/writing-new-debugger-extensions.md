---
title: デバッガーの新しい拡張機能の記述
description: デバッガーの新しい拡張機能の記述
ms.assetid: 6a0d3478-1c7a-44e0-8e48-1334de228c64
keywords:
- 拡張機能コマンド (コマンド) 拡張機能の記述
- 拡張機能コマンドの記述
- dbgeng.h ヘッダー ファイル、拡張機能コマンドの記述
- wdbgexts.h ヘッダー ファイル、拡張機能コマンドの記述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 274e77cd9b973be043f44cce4ca41f4670bc1e4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550428"
---
# <a name="writing-new-debugger-extensions"></a>デバッガーの新しい拡張機能の記述


## <span id="ddk_writing_new_debugger_extensions_dbg"></span><span id="DDK_WRITING_NEW_DEBUGGER_EXTENSIONS_DBG"></span>


拡張 DLL を記述することで、独自のデバッグ コマンドを作成できます。 たとえば、複雑なデータ構造を表示するコマンドまたは停止し、特定の変数またはメモリの場所の値に応じて、ターゲットを開始するコマンドを記述します。

デバッガーの拡張機能の 2 つの異なる種類あります。

-   *拡張機能の DbgEng*します。 これらは、dbgeng.h ヘッダー ファイルでのプロトタイプと wdbgexts.h ヘッダー ファイルもに基づいています。

-   *拡張機能の WdbgExts*します。 これらは、wdbgexts.h ヘッダー ファイルのみでのプロトタイプに基づいています。

デバッガーの拡張機能を記述する方法については、次を参照してください。 [DbgEng 拡張機能の作成](writing-dbgeng-extensions.md)と[WdbgExts 拡張機能の作成](writing-wdbgexts-extensions.md)です。

 

 





