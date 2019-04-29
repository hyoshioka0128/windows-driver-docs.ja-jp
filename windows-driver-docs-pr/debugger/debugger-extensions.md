---
title: デバッガー拡張機能の使用
description: このトピックでは、デバッガーの拡張機能の使用について説明します
ms.assetid: 55de0cbd-c6ba-40af-a932-2f9e57f1e8ec
keywords: 拡張機能コマンドでは、デバッガーの拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61eec47cb84facca4ed21b23f43700d50af9326d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324674"
---
# <a name="using-debugger-extensions"></a>デバッガー拡張機能の使用


## <span id="ddk_debugger_extensions_dbg"></span><span id="DDK_DEBUGGER_EXTENSIONS_DBG"></span>


Visual Studio、WinDbg、KD、および CDB すべては、拡張機能コマンド デバッガーの使用を許可します。 これらの拡張機能は、これら 3 つのマイクロソフトのデバッガー機能と柔軟性の高いを提供します。

デバッガーの拡張機能のコマンドは、標準のデバッガー コマンドと同様に非常に使用されます。 ただし、組み込みのデバッガー コマンドでは、デバッガー バイナリ自体の一部ですが、デバッガーの拡張機能のコマンドは、デバッガーから個別の Dll によって公開されます。

これにより、特定のニーズに対応した新しいデバッガー コマンドを書き込むことができます。 さらに、さまざまなデバッガー拡張機能の Dll は、デバッグに付属するツール自体があります。

このセクションの内容:

[デバッガーの拡張 Dll の読み込み](loading-debugger-extension-dlls.md)

[デバッガーの拡張機能のコマンドを使用します。](using-debugger-extension-commands.md)

[デバッガーの新しい拡張機能の記述](writing-new-debugger-extensions.md)

 

 





