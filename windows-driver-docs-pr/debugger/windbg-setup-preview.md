---
title: WinDbg Preview - とワークスペースの設定
description: このセクションでは、WinDbg プレビュー デバッガーをセットアップする方法について説明します。
ms.date: 08/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64cf7cc9d215afc29e332ea6ee5b5a4fa10ab199
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572778"
---
# <a name="windbg-preview---settings-and-workspaces"></a>WinDbg Preview - とワークスペースの設定

このセクションでは、セットアップし、プレビューの WinDbg デバッガーを構成する方法について説明します。


## <a name="settings"></a>設定

設定メニューを使用して、ソースとシンボルのパスを設定すると、デバッガーのライトと暗いテーマを選択します。 

![新しいフィードバックの追加 ボタンを含むフィードバックのオプションを示すフィードバック ハブのスクリーン ショット](images/windbgx-settings-menu.png)

パスの設定の詳細については、[へのアクセスのデバッグ シンボル](accessing-symbols-for-debugging.md)と[WinDbg でソース コードをデバッグ](source-window.md)を参照してください。

## <a name="workspaces"></a>ワークスペース

ワークスペースを使用すると、ターゲットの接続情報ファイルの構成情報を保存できます。

ワークスペースのオプションは、デバッガーの終了時に保存またはを使用して手動で保存できます*ファイル* -> *ワークスペースの保存*します。 

最近のターゲットの一覧から起動するときにワークスペースが自動的に読み込まれるまたは [ファイル] メニューで手動で読み込むことができます。 

ターゲットの接続情報に加えて、次の設定は、ワークスペース ファイルに格納されます。

#### <a name="general-settings"></a>全般設定 
> [!NOTE]
> このリストと形式は、最終的なし、変更される可能性があります。

設定 | 既定 | 説明
--- | --- | ---
FinalBreak |true | True の場合は、最終的なブレークポイントを無視します (-g コマンド ライン オプション)。
SourceDebugging |true  | ソースまたはアセンブリのモードを切り替えます。
DebugChildProcesses | false| (ユーザー モードのみ)True の場合は、ターゲット アプリケーションによって起動された子プロセスをデバッグします。 (-o コマンド ライン オプション)。
待合室 | false  |  非干渉型指定アタッチ (-pv コマンド ライン オプション)。
NoDebugHeap | false  |  デバッグ ヒープを使用しないように指定します (-hd コマンド ライン オプション)。
Verbose | false  | 詳細モードをオンにすると (登録のダンプ) などのいくつかの表示コマンドは、さらに詳しい出力を生成します。 (-v コマンド ライン オプション)。
昇格 | - |  WinDbg - によって内部的に使用は変更しないでください。
再開可能 | - |  WinDbg - によって内部的に使用は変更しないでください。
UseImplicitCommandLine | false | 使用して暗黙的なコマンド ライン (-cimp コマンド ライン オプション)。 これは、明示的のプロセスを実行するのではなく暗黙的なコマンドラインを使用したデバッガーを開始します。

コマンド ライン オプションの詳細については、[WinDbg コマンド ライン オプション](windbg-command-line-options.md)を参照してください。


#### <a name="symbol-settings"></a>シンボルの設定 

設定 | 既定 | 説明
--- | --- | ---
SymbolOptionsOverride | 0 | 明示的なシンボル オプション定型、1 つの 16 進数値の形式でします。
ShouldOverrideSymbolOptions | false | 場合に設定*true*で指定されたシンボル オプション マスクは、上記で説明した以下のすべてのシンボル オプションをオーバーライドします。
SymOptExactSymbols | false | このオプションは、すべてのシンボル ファイルの厳密な評価を実行するデバッガーです。
SymOptFailCriticalErrors | false | このシンボルのオプションは、抑制する ダイアログ ボックスをファイル アクセス エラーになります。
SymOptIgnoreCvRec | false | このオプションは、シンボルを検索するときに読み込まれたイメージ ヘッダーの CV レコードを無視するシンボル ハンドラーです。 
SymOptIgnoreNtSympath | false | このオプションは、デバッガーでシンボルのパスと実行可能イメージのパスの環境変数の設定を無視します。 
SymOptNoCpp | false | このシンボルのオプションは、C++ の変換をオフにします。 このシンボルのオプションが設定されている場合:: _ _ のすべてのシンボルでは置き換えられます。 
SymOptNoUnqualifiedLoads | false | このシンボルのオプションには、モジュールのシンボル ハンドラーの自動読み込みが無効にします。 このオプションを設定すると、デバッガーがシンボルを照合しようとした場合、既に読み込まれているモジュールのみが検索されます。 
SymOptAutoPublics | false | このシンボルのオプションは、最後の手段としての .pdb ファイルに、パブリック シンボル テーブルを検索する DbgHelp とします。 プライベート シンボル データを検索するときに、一致が見つかった場合、パブリック シンボルは検索されません。 これにより、シンボルの検索の速度が向上します。 
SymOptDebug | false | このシンボルのオプションは、ノイズの多いシンボルの読み込みをオンにします。 これには、デバッガーのシンボルの検索についての情報を表示するように指示します。

シンボルのオプションの詳細については、[シンボル オプション](symbol-options.md)を参照してください。


#### <a name="window-layout-settings"></a>ウィンドウ レイアウトの設定

 ウィンドウ レイアウトでは、グローバルに保存され、ワークスペース ファイルには保存されません。 


#### <a name="workspaces-xml-file"></a>ワークスペースの XML ファイル

ワークスペースとターゲットの接続情報は、XML 形式で格納されます。 

次のファイルは、ワークスペースの構成ファイルの例を示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<TargetConfig Name="C:\paint.dmp" LastUsed="2017-08-03T21:34:20.1013837Z">
  <EngineConfig />
  <EngineOptions>
    <Property name="FinalBreak" value="true" />
    <Property name="SourceDebugging" value="true" />
    <Property name="DebugChildProcesses" value="false" />
    <Property name="Noninvasive" value="false" />
    <Property name="NoDebugHeap" value="false" />
    <Property name="Verbose" value="false" />
    <Property name="SymbolOptionsOverride" value="0" />
    <Property name="ShouldOverrideSymbolOptions" value="false" />
    <Property name="SymOptExactSymbols" value="false" />
    <Property name="SymOptFailCriticalErrors" value="false" />
    <Property name="SymOptIgnoreCvRec" value="false" />
    <Property name="SymOptIgnoreNtSympath" value="false" />
    <Property name="SymOptNoCpp" value="false" />
    <Property name="SymOptNoUnqualifiedLoads" value="false" />
    <Property name="SymOptAutoPublics" value="false" />
    <Property name="SymOptDebug" value="false" />
    <Property name="Elevate" value="false" />
    <Property name="Restartable" value="true" />
    <Property name="UseImplicitCommandLine" value="false" />
  </EngineOptions>
  <TargetOptions>
    <Option name="OpenDump">
      <Property name="DumpPath" value="C:\paint.dmp" />
    </Option>
  </TargetOptions>
</TargetConfig>
```

このファイル形式が WinDbg プレビュー デバッガーにより多くの機能が追加されるときに進化し続けることに注意してください。


---

## <a name="see-also"></a>関連項目

[WinDbg のプレビューを使用したデバッグ](debugging-using-windbg-preview.md)






