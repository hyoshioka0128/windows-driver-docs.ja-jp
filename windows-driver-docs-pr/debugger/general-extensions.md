---
title: 一般的な拡張機能
description: 一般的な拡張機能
ms.assetid: 99ff4111-9f65-4e3d-beb3-0aa49f35a015
keywords:
- 一般的な拡張機能の拡張機能コマンド (コマンド)
- exts.dll (一般的な拡張機能)
- dbghelp.dll (一般的な拡張機能)
- 一般的な拡張機能 (exts.dll - dbghelp.dll)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a77af36b80803c529eafaf0dc865cce09df67290
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552855"
---
# <a name="general-extensions"></a>一般的な拡張機能


## <span id="ddk_general_extensions_dbg"></span><span id="DDK_GENERAL_EXTENSIONS_DBG"></span>


このセクションでは、ユーザー モードおよびカーネル モードのデバッグ中によく使われる拡張機能のコマンドについて説明します。

デバッガーでは、これらの拡張機能コマンドの適切なバージョンが自動的に読み込まれます。 別のバージョンを手動で読み込んだ場合を除き、使用されている DLL のバージョンを追跡する必要はありません。 既定のモジュールの検索順序の詳細については、[デバッガー拡張機能コマンドの使用](using-debugger-extension-commands.md)を参照してください。 拡張機能モジュールを読み込む方法の詳細については、[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)を参照してください。

各拡張機能のコマンド リファレンスのトピックでは、そのコマンドを公開する Dll が一覧表示します。 次の規則を使用して、この拡張 DLL を読み込む適切なディレクトリを特定するから。

-   対象のコンピューターが Microsoft Windows XP または Windows の以降のバージョンを実行している場合を使用して、winxp\\kdexts.dll、winxp\\ntsdexts.dll、winxp\\exts.dll、winext\\ext.dll、または dbghelp.dll します。

 

 





