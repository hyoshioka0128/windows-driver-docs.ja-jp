---
title: デバッガーの拡張 Dll の読み込み
description: デバッガーの拡張 Dll の読み込み
ms.assetid: 6ca70732-cbf6-44fd-a020-c297b40d41f6
keywords:
- 拡張機能コマンド (コマンド) の読み込み
- 拡張機能コマンドの読み込み
- nt4fre ディレクトリ
- nt4chk ディレクトリ
- w2kfre ディレクトリ
- w2kchk ディレクトリ
- winxp ディレクトリ
- winext ディレクトリ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 923e30c897fb96983f7b78e9d265528c1d846690
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539344"
---
# <a name="loading-debugger-extension-dlls"></a>デバッガーの拡張 Dll の読み込み


## <span id="ddk_loading_debugger_extension_dlls_dbg"></span><span id="DDK_LOADING_DEBUGGER_EXTENSION_DLLS_DBG"></span>


デバッガーの拡張 Dll の読み込みと既定のデバッガー拡張 DLL と既定のデバッガー拡張機能のパスを制御するいくつかの方法はあります。

-   (前に、デバッガーを開始)使用して、 \_NT\_デバッガー\_拡張子\_パス[環境変数](environment-variables.md)拡張 Dll の既定のパスを設定します。 さまざまなディレクトリ パスをセミコロンで区切って指定できます。

-   使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md)新しい DLL を読み込むコマンド。

-   使用して、 [ **.unload (拡張 DLL のアンロード)** ](-unload--unload-extension-dll-.md) DLL をアンロードするコマンド。

-   使用して、 [ **.unloadall (すべての拡張 Dll のアンロード)** ](-unloadall--unload-all-extension-dlls-.md)デバッガーのすべての拡張機能をアンロードするコマンド。

-   (デバッガーを開始する前にCDB のみ) 使用して、 [tools.ini](configuring-tools-ini.md)ファイルを既定の拡張 DLL を設定します。

-   (前に、デバッガーを開始)使用して、 **-** [コマンド ライン オプション](command-line-options.md)DLL 既定の拡張機能を設定します。

-   使用して、 [ **.extpath (拡張機能の設定パス)** ](-extpath--set-extension-path-.md)拡張 DLL の検索パスを設定するコマンド。

-   使用して、 [ **.setdll (既定拡張 DLL の設定)** ](-setdll--set-default-extension-dll-.md)既定拡張 DLL を設定するコマンド。

-   使用して、 [ **.chain (リスト デバッガー拡張)** ](-chain--list-debugger-extensions-.md)の既定の検索順序で読み込まれたデバッガー拡張機能のすべてのモジュールを表示するコマンド。

完全なを使用するだけで、拡張 DLL を読み込むことも **!**<em>モジュール</em>**.**<em>拡張子</em>モジュールからコマンドを発行する 1 つ目の構文にします。 参照してください[デバッガー拡張機能コマンドの使用](using-debugger-extension-commands.md)詳細についてはします。

拡張機能を使用する Dll は、ターゲット コンピューターのオペレーティング システムと一致する必要があります。 拡張ツールを Windows のデバッグ パッケージに付属する Dll は、各インストール ディレクトリの別のサブディレクトリに配置されています。

-   Winxp ディレクトリには、Windows XP 以降のバージョンの Windows で使用できる拡張機能が含まれています。

-   Winext ディレクトリには、任意のバージョンの Windows で使用できる拡張機能が含まれています。 Windows のツールをデバッグの基本ディレクトリにある、dbghelp.dll モジュールには、この型の拡張機能も含まれます。

独自のデバッガー拡張機能を記述する場合は、任意のディレクトリに配置できます。 ただし、新しいディレクトリに配置し、デバッガーの拡張機能のパスをそのディレクトリを追加するをお勧めします。

最大 32 の拡張 Dll が読み込まれることができます。

 

 





