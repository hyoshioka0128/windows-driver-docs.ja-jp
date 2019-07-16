---
title: GFlags の詳細
description: GFlags の詳細
ms.assetid: 97faa63d-b876-4973-812f-f3bdd57c1778
keywords:
- GFlags、詳細情報
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 858425dd05b286a6d2584acee7185a8e50828a9b
ms.sourcegitcommit: 707739250ebdcd74a26d85d8b4217fa81c9c9e95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68181281"
---
# <a name="gflags-details"></a>GFlags の詳細

GFlags ができ、Windows レジストリと内部の設定を編集することによってシステムの機能を無効にします。 このセクションでは、GFlags の操作の詳細を説明し、GFlags を最も効率的に使用するためのヒントが含まれています。

## <a name="general-information"></a>一般情報

- コマンドラインで、GFlags ダイアログ ボックスを表示する次のように入力します。 **gflags** (パラメーターなし) を使用します。

- GFlags システム レベルのレジストリ設定はレジストリには、すぐに表示が有効になりません、システムを再起動するまで。

- GFlags イメージ ファイルのレジストリ設定はレジストリには、すぐに表示が有効になりませんプロセスを再起動するまで。

- GFlags ダイアログ ボックスで、デバッガーと起動の機能は、特定のプログラムです。 のみ設定できますに 1 つのイメージ ファイルを一度に。

### <a name="flag-details"></a>フラグの詳細

- すべてのフラグをクリアするには、-FFFFFFFF に、フラグを設定します。 0 に、フラグを設定すると、現在のフラグ値に 0 が追加されます。

- Windows イメージ ファイルのすべてのフラグをクリアし、削除 FFFFFFFF (0 xffffffff) にイメージ ファイルのフラグを設定すると、 **GlobalFlag**イメージ ファイルのレジストリ キー エントリ。 イメージ ファイルのレジストリ キーが保持されます。

### <a name="dialog-box-and-command-line"></a>ダイアログ ボックスとコマンドライン

GFlags、便利なダイアログ ボックスを使用するか、コマンドラインから実行できます。 ほとんどの機能が、次の例外の両方の形式で利用できます。

#### <a name="dialog-box-only"></a>ダイアログ ボックスのみ

- 起動します。 指定したフラグを使用してプログラムを起動します。

- デバッガーでプログラムを実行します。

- [特別なプール](special-pool.md)Windows Vista より前のシステムにします。 Windows Vista および Windows の以降のバージョンでは、コマンドラインまたは Gflags ダイアログ ボックスで、特別なプール機能を構成できます。

#### <a name="command-line-only"></a>コマンドラインのみ

- ユーザー モードのスタック トレースのデータベースのサイズを設定 (/tracedb)。

- ページ ヒープの検証オプションを設定します。

### <a name="registry-information"></a>レジストリ情報

セッション間で保存されている GFlags 設定は、レジストリに格納されます。 クエリまたはこれらの値を変更するのには、レジストリ Api、Regedit、または reg.exe を使用できます。 次の表では、設定とレジストリの格納場所の種類を示します。

|設定の種類|レジストリの場所|
|----|----|
|システム全体の設定 ("Registry")|Hkey_local_machine \system\currentcontrolset\control\session Manager\\**GlobalFlag**|
|コンピューターのすべてのユーザーのプログラムに固有の設定 (「画像ファイル」)。|Hkey_local_machine \software\microsoft\windows nt \currentversion\image File Execution Options\\*ImageFileName*\\**GlobalFlag**|
|コンピューターのすべてのユーザーに対して特定のプログラム (「サイレント プロセス終了」) の設定をサイレント終了します。|Hkey_local_machine \software\microsoft\windows NT\CurrentVersion\SilentProcessExit\\***ImageFileName***|
|コンピューターのすべてのユーザーのイメージ ファイルをページ ヒープのオプション|Hkey_local_machine \software\microsoft\windows nt \currentversion\image File Execution Options\\*ImageFileName*\\**PageHeapFlags**
|ユーザー モードのスタック トレースのデータベース サイズ (**tracedb**)|Hklm \software\microsoft\windows nt \currentversion\image File Execution Options\\*ImageFileName*\\**StackTraceDatabaseSizeInMb**|
|ユーザー データベースの作成モード スタック トレース (ust、0x1000) のイメージ ファイル|Windows イメージ ファイル名を USTEnabled レジストリ エントリの値に追加します (hklm \software\microsoft\windows nt \currentversion\image File Execution Options\\**USTEnabled**)。
|Load image using large pages if possible|Hklm \software\microsoft\windows nt \currentversion\image File Execution Options\\*ImageFileName*\\**UseLargePages**します。
|特別なプール (カーネルの特別なプール タグ)|Hklm \system\currentcontrolset\control\session manager \memory Management\\**PoolTag**|
確認の開始/終了を確認します|Hklm \system\currentcontrolset\control\session \memory Management\PoolTagOverruns します。 **開始確認**オプション値を 0 に設定します。 **終了の確認**オプション値を 1 に設定します。
|イメージ ファイルをデバッガー|Hklm \software\microsoft\windows nt \currentversion\image File Execution Options\\*ImageFileName*\\**デバッガー**
|Object Reference Tracing|Hklm \system\currentcontrolset\control\session Manager\Kernel\\**ObTraceProcessName**、 **ObTracePermanent**と**ObTracePoolTags**
