---
title: ユーザー モードの拡張機能
description: ユーザー モードの拡張機能
ms.assetid: 83b0aca1-ad08-4384-a035-3d7bd2c1b4fe
keywords:
- ユーザー モードの拡張機能の拡張機能コマンド (コマンド)
- ntsdexts.dll (ユーザー モードの拡張機能)
- uext.dll (ユーザー モードの拡張機能)
- ユーザー モードの拡張機能 (ntsdexts.dll および uext.dll)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ff392e2c863b60ef2d81d4037929743688814c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581167"
---
# <a name="user-mode-extensions"></a>ユーザー モードの拡張機能


## <span id="ddk_user_mode_extensions_dbg"></span><span id="DDK_USER_MODE_EXTENSIONS_DBG"></span>


参照のこのセクションでは、ユーザー モードのデバッグ中には主に使用される拡張機能のコマンドについて説明します。

デバッガーは、これらの拡張機能コマンドの適切なバージョンを自動的に読み込まれます。 別のバージョンを手動で読み込んだ場合を除き、使用されている DLL のバージョンを追跡する必要はありません。 参照してください[デバッガー拡張機能コマンドの使用](using-debugger-extension-commands.md)の既定のモジュールの検索順序の説明。 参照してください[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)拡張モジュールを読み込む方法の詳細について。

各拡張機能のコマンド リファレンスのページには、そのコマンドを公開する Dll が一覧表示します。 この拡張 DLL の読み込み元となる適切なディレクトリを特定するのにには、次の規則を使用します。

-   ターゲット アプリケーションが Windows XP または Windows の以降のバージョンで実行している場合を使用して、winxp\\Ntsdexts.dll します。

さらに、任意の 1 つのオペレーティング システムに固有ではないユーザー モードの拡張機能で見つかる winext\\Uext.dll します。

 

 





