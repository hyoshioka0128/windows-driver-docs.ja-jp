---
title: WinDbg プレビュー-設定とワークスペース
description: ここでは、WinDbg preview デバッガーを設定する方法について説明します。
ms.date: 01/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8f7b6a4d0987326e509aa20a5c82d3d51400f5f4
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256739"
---
# <a name="windbg-preview---settings-and-workspaces"></a>WinDbg プレビュー-設定とワークスペース

![ビットパターンを使用した windbg プレビューの小さいロゴ](images/windbgx-preview-logo.png)

ここでは、WinDbg Preview デバッガーを設定して構成する方法について説明します。

## <a name="settings"></a>設定

[設定] メニューを使用して、ソースパスやシンボルパスなどを設定したり、デバッガーの明るいテーマとダークテーマを選択したりします。 

![[全般] タブを表示する設定のスクリーンショット](images/windbgx-settings-menu.png)

現在、6つの設定ダイアログパネルがあります。

- [全般]
- コマンド ウィンドウ
- デバッグ設定
- 逆アセンブリウィンドウ
- イベント & 例外
- ソース ウィンドウ

パスの設定の詳細については、「 [WinDbg でデバッグおよびソースコードのデバッグ](source-window.md)[を行うためのシンボルへのアクセス](accessing-symbols-for-debugging.md)」を参照してください。

## <a name="workspaces"></a>ワークスペース

ワークスペースでは、ターゲット接続情報ファイルに構成情報を保存できます。

ワークスペースのオプションは、デバッガーを終了したときに保存されます。または、*ファイル* -> *保存* を使用して手動で保存することもできます。 

ワークスペースは、[最近のターゲット] の一覧から起動するときに自動的に読み込まれるか、または [ファイル] メニューに手動で読み込むことができます。 

ターゲット接続情報に加えて、次の設定がワークスペースファイルに格納されます。

#### <a name="general-settings"></a>[General Settings]

> [!NOTE]
> この一覧と形式は最終的なものではなく、変更される可能性があります。

設定 | 既定 | 説明
--- | --- | ---
FinalBreak |true | True の場合、最後のブレークポイント (-g コマンドラインオプション) は無視されます。
SourceDebugging |true  | ソースモードまたはアセンブリモードを切り替えます。
DebugChildProcesses | false| (ユーザーモードのみ)True の場合、ターゲットアプリケーションによって起動される子プロセスをデバッグします。 (-o コマンドラインオプション)。
Noninvasive | false  |  非干渉の attach (-pv コマンドラインオプション) を指定します。
NoDebugHeap | false  |  デバッグヒープを使用しないことを指定します (-hd コマンドラインオプション)。
Verbose | false  | 詳細モードが有効になっていると、一部の表示コマンド (レジスタダンプなど) でより詳細な出力が生成されます。 (-v コマンドラインオプション)。
昇格 | - |  WinDbg によって内部的に使用されます。変更しないでください。
Dbms | - |  WinDbg によって内部的に使用されます。変更しないでください。
UseImplicitCommandLine | false | 暗黙のコマンドラインを使用します (-cimp コマンドラインオプション)。 これにより、明示的な実行プロセスではなく、暗黙的なコマンドラインを使用してデバッガーが起動されます。

コマンドラインオプションの詳細については、「 [WinDbg のコマンドラインオプション](windbg-command-line-options.md)」を参照してください。

#### <a name="symbol-settings"></a>[シンボルの設定]

設定 | 既定 | 説明
--- | --- | ---
SymbolOptionsOverride | 0 | 1つの16進数の形式の明示的なシンボルオプションマスク。
ShouldOverrideSymbolOptions | false | *True*に設定すると、上記で説明したシンボルオプションマスクを使用して、以下に示すシンボルオプションがすべてオーバーライドされます。
SymOptExactSymbols | false | このオプションを指定すると、デバッガーはすべてのシンボルファイルの厳密な評価を実行します。
SymOptFailCriticalErrors | false | このシンボルオプションを使用すると、ファイルアクセスエラーのダイアログボックスが表示されなくなります。
SymOptIgnoreCvRec | false | このオプションを指定すると、シンボルの検索時に、読み込まれたイメージヘッダーの CV レコードがシンボルハンドラーによって無視されます。 
SymOptIgnoreNtSympath | false | このオプションを指定すると、シンボルパスと実行可能イメージパスの環境変数の設定がデバッガーによって無視されます。 
SymOptNoCpp | false | このシンボルオプションは、 C++翻訳をオフにします。 この記号オプションが設定されている場合、:: はすべての記号で __ に置き換えられます。 
SymOptNoUnqualifiedLoads | false | このシンボルオプションは、シンボルハンドラーによるモジュールの自動読み込みを無効にします。 このオプションを設定し、デバッガーがシンボルとの照合を試みると、既に読み込まれているモジュールだけが検索されます。 
SymOptAutoPublics | false | このシンボルオプションを使用すると、最新の手段としてのみ .pdb ファイル内のパブリックシンボルテーブルを検索できます。 プライベートシンボルデータの検索時に一致するものが見つかった場合、パブリックシンボルは検索されません。 これにより、シンボル検索速度が向上します。 
SymOptDebug | false | このシンボルオプションは、ノイズの多いシンボルの読み込みを有効にします。 これは、シンボルの検索に関する情報を表示するようにデバッガーに指示します。

シンボルオプションの詳細については、「[シンボルオプション](symbol-options.md)」を参照してください。

#### <a name="window-layout-settings"></a>ウィンドウレイアウトの設定

 ウィンドウレイアウトはグローバルに保存され、ワークスペースファイルには保存されません。 

#### <a name="workspaces-xml-file"></a>ワークスペースの XML ファイル

ワークスペースとターゲットの接続情報は、XML 形式で格納されます。

次のファイルは、ワークスペース構成ファイルの例を示しています。

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

このファイル形式は、WinDbg Preview デバッガーに追加される機能が増えるにつれて進化し続けていることに注意してください。

---

## <a name="see-also"></a>関連項目

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)
