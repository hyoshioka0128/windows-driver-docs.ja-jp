---
title: カーネル モードの拡張機能
description: カーネル モードの拡張機能
ms.assetid: e8e1e692-d991-427f-a2e7-b9eb1893fe83
keywords:
- 拡張機能のコマンド (コマンド)、カーネル モードの拡張機能
- kdextx86.dll (カーネル モードの拡張機能)
- kdexts.dll (カーネル モードの拡張機能)
- kext.dll (カーネル モードの拡張機能)
- カーネル モードの拡張機能 (kdext .dll および kext.dll)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61a97b92cb83e2a304bdfc7d4300eb415cdb87f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367185"
---
# <a name="kernel-mode-extensions"></a>カーネル モードの拡張機能


## <span id="ddk_kernel_mode_extensions_dbg"></span><span id="DDK_KERNEL_MODE_EXTENSIONS_DBG"></span>


参照のこのセクションでは、カーネル モードのデバッグ中には主に使用される拡張機能のコマンドについて説明します。

デバッガーは、これらの拡張機能コマンドの適切なバージョンを自動的に読み込まれます。 別のバージョンを手動で読み込んだ場合を除き、使用されている DLL のバージョンを追跡する必要はありません。 参照してください[デバッガー拡張機能コマンドの使用](using-debugger-extension-commands.md)の既定のモジュールの検索順序の説明。 参照してください[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)拡張モジュールを読み込む方法の詳細について。

各拡張機能のコマンド リファレンスのページには、そのコマンドを公開する Dll が一覧表示します。 この拡張 DLL の読み込み元となる適切なディレクトリを特定するのにには、次の規則を使用します。

-   対象のコンピューターが Windows XP または Windows の以降のバージョンを実行している場合を使用して、winxp\\Kdexts.dll します。

さらに、任意の 1 つのオペレーティング システムに固有でないカーネル モードの拡張機能で見つかる winext\\kext.dll します。

 

 





