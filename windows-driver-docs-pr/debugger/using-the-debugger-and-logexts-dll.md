---
title: デバッガーと Logexts.dll を使用してください。
description: デバッガーと Logexts.dll を使用してください。
ms.assetid: 7f7d3ca2-9b40-41ce-b66c-4367b93a7ff7
keywords:
- Logger, logexts.dll
- ロガー、CDB
- Logger, WinDbg
- logexts.dll
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1538080047adc6ac27e8868268b2673e23e37c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531779"
---
# <a name="using-the-debugger-and-logextsdll"></a>デバッガーと Logexts.dll を使用してください。


## <span id="ddk_using_the_debugger_and_logexts_dll_dtoolq"></span><span id="DDK_USING_THE_DEBUGGER_AND_LOGEXTS_DLL_DTOOLQ"></span>


ロガーをアクティブ化する方法の 1 つが、CDB または WinDbg を起動し、ユーザー モードの対象アプリケーションを通常どおりに接続します。 次に、使用、 [ **! logexts.logi** ](-logexts-logi.md)または[ **! logexts.loge** ](-logexts-loge.md)拡張機能コマンド。

オフの読み込みと Logexts.dll をターゲット アプリケーションのプロセスの初期化ルーチンにジャンプは、現在のブレークポイントでコードが挿入されます。 「ロガーは、ターゲット アプリケーションに挿入」と呼ばれる

このモジュールは、デバッガー拡張 DLL と、プログラム、ターゲット アプリケーションに挿入されるため、Logexts.dll の実行中の 2 つのインスタンス実際になります。 Logexts.dll のデバッガーとターゲットのインスタンスは、出力ファイルのハンドル、現在のカテゴリのマスク、およびログの出力バッファーへのポインターを含むメモリの共有セクションを介して通信します。

### <a name="span-idattachingtothetargetapplicationspanspan-idattachingtothetargetapplicationspanattaching-to-the-target-application"></a><span id="attaching_to_the_target_application"></span><span id="ATTACHING_TO_THE_TARGET_APPLICATION"></span>ターゲット アプリケーションへのアタッチ

ターゲット アプリケーションにデバッガーをアタッチする方法については、次を参照してください。[ユーザー モード プロセスを使用して WinDbg をデバッグ](debugging-a-user-mode-process-using-windbg.md)または[デバッグ ユーザー モード プロセスを使用して CDB](debugging-a-user-mode-process-using-cdb.md)します。

### <a name="span-idusingtheloggerextensioncommandsspanspan-idusingtheloggerextensioncommandsspanusing-the-logger-extension-commands"></a><span id="using_the_logger_extension_commands"></span><span id="USING_THE_LOGGER_EXTENSION_COMMANDS"></span>ロガー拡張機能のコマンドを使用します。

各拡張機能の完全な構文、その参照ページを参照してください。

<span id="_LOGEXTS.LOGI"></span>[**!logexts.logi**](-logexts-logi.md)  
ターゲット アプリケーションには、ロガーを挿入します。 これは、ログ記録を初期化しますが、これを有効にしません。

<span id="_LOGEXTS.LOGE"></span>[**!logexts.loge**](-logexts-loge.md)  
ログを有効にします。 場合[ **! logexts.logi** ](-logexts-logi.md)されていません。 使用すると、この拡張機能は初期化し、ログ記録を有効にします。

<span id="_LOGEXTS.LOGD"></span>[**!logexts.logd**](-logexts-logd.md)  
ログ記録を無効にします。 これにより、プログラムを自由に実行を許可する取り組みの一環として削除するすべての API フック。 再度有効にすることはできませんので、COM のフックは削除されません。

<span id="_LOGEXTS.LOGO"></span>[**!logexts.logo**](-logexts-logo.md)  
表示または出力オプションを変更します。 次の 3 つの種類の出力が可能です。 デバッガー、テキスト ファイル、または .lgv ファイルに直接送信されるメッセージ。 .Lgv ファイルには、他の 2 つの; よりもより多くの情報が含まれています。読み取ることができる[LogViewer](logviewer.md)します。

テキスト ファイルの出力を無効にした場合サイズがゼロの .txt ファイルが作成されます。 これにより、同じ場所に以前に保存したテキスト ファイルが上書きされます。

<span id="_LOGEXTS.LOGC"></span>[**!logexts.logc**](-logexts-logc.md)  
利用可能な API のカテゴリ、カテゴリが記録され、これは使用されませんコントロールを表示し、任意のカテゴリに含まれる Api を表示します。

カテゴリが無効になっている場合、パフォーマンスのオーバーヘッドが不要になったようにそのカテゴリ内のすべての Api のフックは削除されます。 再度有効にすることはできませんので、COM のフックは削除されません。

特定のカテゴリのみを有効にするは、プログラムが Windows - たとえば、ファイル操作で発生している操作の特定の種類で関心のみときに役立ちます。 これにより、ログ ファイルのサイズを減少し、ロガーがプロセスの実行速度に与える影響も減少します。

<span id="_LOGEXTS.LOGB"></span>[**!logexts.logb**](-logexts-logb.md)  
表示または現在の出力バッファーをフラッシュします。 パフォーマンスの考慮事項としては、ログ出力は出力バッファーが完全な場合にのみディスクにフラッシュされます。 既定では、バッファーは、2144 バイトです。

バッファー メモリは、対象のアプリケーションで管理される、ため、アクセス違反またはいくつかその他の回復できないエラーで、ターゲット アプリケーションである場合、ディスク上のログ ファイルのバッファーの自動作成は発生しません。 このような場合、このコマンドは、手動で、ディスクにバッファーをフラッシュを使用する必要があります。 そうしないログ ファイルで最も最近記録された Api がされない可能性があります。

<span id="_LOGEXTS.LOGM"></span>[**!logexts.logm**](-logexts-logm.md)  
表示またはモジュールの包含/除外リストを作成します。 多くの場合のみモジュールまたは一連のモジュールから行われたこれらの API 呼び出しをログ記録する必要があります。 ロガーでは、容易にするために、モジュールの一覧、または代わりに、モジュールの除外リストを指定できます。 たとえば、1 つまたは 2 つのモジュールからの呼び出しをログ記録たい場合は、信頼のリストを使用します。 モジュールの短い一覧を除くすべてのモジュールからの呼び出しを記録したい場合は、除外リストを使用します。 Logexts.dll と Kernel32.dll のモジュールはロガーはログ自体に許可されていませんので常に除外します。

 

 





