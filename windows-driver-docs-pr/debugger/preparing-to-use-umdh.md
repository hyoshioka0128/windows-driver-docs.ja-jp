---
title: UMDH を使用する準備
description: UMDH を使用する準備
ms.assetid: 9adebe43-3167-4e1a-ac98-db19ace944be
keywords:
- UMDH、UMDH を使用する準備
- UMDH、BSTR のキャッシュを無効にします。
- SetNoOaCache 関数
- OANOCACHE 環境変数
- スタック トレースのデータベース
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6614f26f908dea52edbf0b1d8a71bf0ae618135
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558430"
---
# <a name="preparing-to-use-umdh"></a>UMDH を使用する準備


## <span id="ddk_preparing_to_use_umdh_dtools"></span><span id="DDK_PREPARING_TO_USE_UMDH_DTOOLS"></span>


ユーザー モード ダンプ ヒープ (UMDH) を使用して、プロセスのヒープ割り当てをキャプチャする前に、このセクションで説明した構成タスクを完了する必要があります。 コンピューターが正しく構成されていない場合 UMDH はすべての結果を生成しませんまたは結果が不完全または不正確になります。

### <a name="span-idcreatetheusermodestacktracedatabasespanspan-idcreatetheusermodestacktracedatabasespancreate-the-user-mode-stack-trace-database"></a><span id="create_the_user_mode_stack_trace_database"></span><span id="CREATE_THE_USER_MODE_STACK_TRACE_DATABASE"></span>ユーザー モードのスタック トレースのデータベースを作成します。

プロセスのヒープ割り当てをキャプチャする UMDH を使用する前に、スタック トレースをキャプチャする Windows を構成する必要があります。

プロセスのスタック トレースのキャプチャを有効にするには、 [GFlags](gflags.md)を設定する、**ユーザー モードのスタック トレースのデータベースの作成**プロセスのフラグ。 これは、次のいずれかで実行できます。

-   GFlags、グラフィカル インターフェイスでは、選択、**イメージ ファイル**タブ。ファイル名拡張子 (例: Notepad.exe) を含む、プロセス名を入力します。 キーを押して、**タブ**キーを選択します**ユーザー モードのスタック トレースのデータベースの作成**、 をクリックし、**適用**します。

-   または、同等に、次の GFlags コマンドラインを使用している*ImageName* (ファイル名拡張子を含む)、プロセス名には。

    **gflags/i** *ImageName* **+ ust**

Windows を収集するスタック トレース データの量が x86 32 MB に制限は既定では、プロセッサ、および 64 MB、x64 プロセッサ。 このデータベースのサイズを大きく必要があります場合、選択、**イメージ ファイル**GFlags グラフィック インターフェイスでタブで、プロセス名を入力キーを押して、**タブ**、キーのチェック、 **Stack Backtrace (メガバイト)** チェック ボックスをオン、関連付けられているテキスト ボックスで、(単位は MB) の値を入力してクリックして、**適用**します。

**注**  限られた Windows リソースが消費されますが、ため、必要な場合にのみ、このデータベースが向上します。 サイズが大きくなる必要がなくなったには、元の値にこの設定を返します。

 

これらの設定では、プログラムのすべての新しいインスタンスに影響します。 プログラムの現在実行中のインスタンスには影響しません。

### <a name="span-idaccessthenecessarysymbolsspanspan-idaccessthenecessarysymbolsspanaccess-the-necessary-symbols"></a><span id="access_the_necessary_symbols"></span><span id="ACCESS_THE_NECESSARY_SYMBOLS"></span>必要なシンボルにアクセスします。

UMDH を使用する前に、アプリケーションの適切なシンボルへのアクセスが必要です。 UMDH 環境変数で指定されたシンボル パスを使用して\_NT\_シンボル\_パス。 この変数に格納をアプリケーションのシンボルを含むパスに設定します。

Windows シンボルへのパスを含めることも、分析がより詳細な可能性があります。 このシンボル パスの構文は、デバッガーによって使用されるのと同じ詳細については、[シンボル パス](symbol-path.md)を参照してください。

たとえば、アプリケーションのシンボルは c:\\MyApp\\記号、およびをインストールする Windows シンボル ファイル\\ \\myshare\\winsymbols、以下を使用する場合シンボル パスを設定するコマンド:

```console
set _NT_SYMBOL_PATH=c:\myapp\symbols;\\myshare\winsymbols
```

アプリケーションのシンボルが c: である場合は、別の例として\\MyApp\\記号とする、c: を使用して、Windows シンボルのパブリックの Microsoft シンボル ストアを使用する場合\\、ダウン ストリームのストアとして MyCache します。シンボル パスを設定するのに次のコマンドを使用します。

```console
set _NT_SYMBOL_PATH=c:\myapp\symbols;srv*c:\mycache*https://msdl.microsoft.com/download/symbols
```

**重要な**  2 台のコンピューターがあるとします。、*コンピューターへのログオン*UMDH ログを作成すると、*分析コンピューター* UMDH ログを分析します。 分析のコンピューター上のシンボル パスは、ログが行われた時にログ記録のコンピューターに読み込まれている Windows のバージョンのシンボルを指す必要があります。 シンボル サーバーを分析コンピューターにシンボル パスを指していません。 場合は、UMDH は分析のコンピューターで実行されている Windows のバージョンのシンボルを取得し、UMDH に意味のある結果は表示されません。

 

### <a name="span-iddisablebstrcachingspanspan-iddisablebstrcachingspandisable-bstr-caching"></a><span id="disable_bstr_caching"></span><span id="DISABLE_BSTR_CACHING"></span>BSTR のキャッシュを無効にします。

オートメーション (以前の OLE オートメーション) では、BSTR 文字列によって使用されるメモリをキャッシュします。 これにより、UMDH で正しくメモリ割り当ての所有者を決定するようにできます。 この問題を回避するには、BSTR のキャッシュを無効にする必要があります。

BSTR のキャッシュを無効にするには、(1) を 1 に等しい OANOCACHE の環境変数を設定します。 この設定は、その割り当てをトレースするアプリケーションを起動する前に行う必要があります。

BSTR のキャッシュから、アプリケーション自体に .NET Framework を呼び出すことによって無効にする代わりに、 **SetNoOaCache**関数。 この方法を選択する場合はこの関数を呼び出す早い段階でため BSTR 割り当て済みのときにキャッシュされている**SetNoOaCache**が呼び出されますがキャッシュに残ったままです。

サービスによって行われた割り当てを追跡する必要がある場合は、システム環境変数として OANOCACHE を設定しを有効にするこの設定の Windows を再起動する必要があります。

Windows 2000 では、に加えて OANOCACHE を 1 に、設定する必要がありますも、修正プログラムのインストールで使用可能な[Microsoft サポート記事 139071](https://go.microsoft.com/fwlink/p/?LinkId=241583)します。 この修正プログラムは、Windows XP と Windows の以降のバージョンでは必要ありません。

### <a name="span-idfindtheprocessidspanspan-idfindtheprocessidspanfind-the-process-id"></a><span id="find_the_process_id"></span><span id="FIND_THE_PROCESS_ID"></span>プロセス ID が見つかりません

UMDH では、そのプロセス id (PID) で、プロセスを識別します。 Tasklist、タスク マネージャーを使用して、実行中のプロセスの PID を検索することができますか[TList](tlist.md)します。

 

 





