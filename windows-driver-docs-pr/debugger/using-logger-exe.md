---
title: Logger.exe の使用
description: Logger.exe の使用
ms.assetid: da2ec999-4529-49dc-855e-a7d3b15583f7
keywords:
- ロガー、logger.exe
- logger.exe
- ロガーのスタンドアロン
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc67028c19a1575721470d7f438981a64b890978
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581182"
---
# <a name="using-loggerexe"></a>Logger.exe の使用


## <span id="ddk_using_logger_exe_dtoolq"></span><span id="DDK_USING_LOGGER_EXE_DTOOLQ"></span>


ロガーをアクティブ化する方法の 1 つでは、スタンドアロンの Logger.exe プログラムを実行します。 これは、1 つのターゲットを受け取ることができる非常に小さいデバッガー本質的にです。 で実行するには、コマンドラインでターゲット アプリケーションの名前を含めます。

```dbgcmd
logger Target 
```

これがアクティブになる、指定したアプリケーションの読み込み、オフの読み込みと Logexts.dll をターゲット アプリケーションのプロセスの初期化ルーチンにジャンプするターゲット アプリケーションにコードが挿入されます。 「ロガーは、ターゲット アプリケーションに挿入」と呼ばれる

Logger.exe ユーティリティと Logexts.dll モジュールは、このロガーの車両の 2 つのコンポーネントです。 出力ファイルのハンドル、現在のカテゴリのマスク、およびログの出力バッファーへのポインターを含むメモリの共有セクションを介して通信します。

タイトルのウィンドウ**ロガー (デバッガー)** が表示されます。 このウィンドウには、ロガーの進行状況が表示されます。

### <a name="span-idchangesettingsdialogboxspanspan-idchangesettingsdialogboxspanchange-settings-dialog-box"></a><span id="change_settings_dialog_box"></span><span id="CHANGE_SETTINGS_DIALOG_BOX"></span>設定の変更 ダイアログ ボックス

初期化が完了すると、最初の表示が完了したら、後に、**設定の変更** ダイアログ ボックスが表示されます。 これにより、ロガーの設定を構成することができます。 さまざまな設定を次に示します。

<span id="API_Settings"></span><span id="api_settings"></span><span id="API_SETTINGS"></span>**API 設定**  
この一覧には、利用可能な API のカテゴリが表示されます。 強調表示されているカテゴリをログに記録されます。強調表示されている非カテゴリにはありません。 初めて、ロガーを実行するすべてのカテゴリがハイライトされます。 ただし、以降の実行でロガーはの追跡、指定したターゲット アプリケーションに対してどのカテゴリを選択します。

カテゴリが無効になっている場合、パフォーマンスのオーバーヘッドが不要になったようにそのカテゴリ内のすべての Api のフックは削除されます。 再度有効にすることはできませんので、COM のフックは削除されません。

特定のカテゴリのみを有効にするは、プログラムが Windows - たとえば、ファイル操作で発生している操作の特定の種類で関心のみときに役立ちます。 これにより、ログ ファイルのサイズを減少し、ロガーがプロセスの実行速度に与える影響も減少します。

<span id="Logging"></span><span id="logging"></span><span id="LOGGING"></span>**ログ記録**  
このセクションが含まれています**を有効にする**と**を無効にする**ラジオ ボタン。 ログ記録を無効にすると、プログラムを自由に実行を許可する取り組みの一環として削除するすべての API フックが発生します。 再度有効にすることはできませんので、COM のフックは削除されません。

<span id="Inclusion___Exclusion_List"></span><span id="inclusion___exclusion_list"></span><span id="INCLUSION___EXCLUSION_LIST"></span>**包含/除外の一覧**  
このセクションでは、モジュールの包含/除外リストを制御します。 特定のモジュールまたは一連のモジュールから行われた関数の呼び出しのみを記録することが望ましいです。 ロガーでは、容易にするために、モジュールの一覧、または代わりに、モジュールの除外リストを指定できます。 たとえば、1 つまたは 2 つのモジュールからの呼び出しをログ記録たい場合は、信頼のリストを使用します。 モジュールの短い一覧を除くすべてのモジュールからの呼び出しを記録したい場合は、除外リストを使用します。 Logexts.dll と Kernel32.dll のモジュールはロガーはログ自体に許可されていませんので常に除外します。

<span id="Flush_the_Buffer"></span><span id="flush_the_buffer"></span><span id="FLUSH_THE_BUFFER"></span>**バッファーをフラッシュします。**  
このボタンは、現在の出力バッファーがフラッシュされます。 パフォーマンスの考慮事項としては、ログ出力は出力バッファーが完全な場合にのみディスクにフラッシュされます。 既定では、バッファーは、2144 バイトです。

バッファー メモリは、対象のアプリケーションで管理される、ため、アクセス違反またはいくつかその他の回復できないエラーで、ターゲット アプリケーションである場合、ディスク上のログ ファイルのバッファーの自動作成は発生しません。 このような場合は、ターゲット アプリケーションのウィンドウをアクティブにし、このダイアログ ボックスを取得し、キーを押します f12 キーを押すとする必要があります**バッファーをフラッシュ**します。 これが行われていない場合、最も最近記録された関数可能性があります、ログ ファイルには表示されません。

<span id="Go"></span><span id="go"></span><span id="GO"></span>**移動**  
これにより、対象のアプリケーションの実行を開始します。

### <a name="span-idrunningthetargetapplicationspanspan-idrunningthetargetapplicationspanrunning-the-target-application"></a><span id="running_the_target_application"></span><span id="RUNNING_THE_TARGET_APPLICATION"></span>ターゲット アプリケーションを実行します。

設定を選択したら、クリックして**移動**します。 ダイアログ ボックスが閉じられ、ターゲット アプリケーションの実行を開始します。

ターゲット アプリケーションのウィンドウをアクティブにして f12 キーを押す場合は、ロガーに中断されます。 これにより、固定するのには、ターゲット アプリケーションと**設定の変更** ダイアログ ボックスが再度表示します。 設定を変更するには、キーを押し、必要に応じて場合**移動**の実行を続行します。

実行する限り、対象アプリケーションをさせることができます。 通常モードまたはエラーのためを終了する場合、ログ記録が停止し、再起動することはできません。

を終了するときに選択**ファイル |終了**クリック**はい**します。 ターゲット アプリケーションがまだ実行されている場合は終了します。

### <a name="span-idlimitationsofloggerexespanspan-idlimitationsofloggerexespanlimitations-of-loggerexe"></a><span id="limitations_of_logger_exe"></span><span id="LIMITATIONS_OF_LOGGER_EXE"></span>Logger.exe の制限事項

ロガー Logger.exe ツールを実行しているときに、.lgv ファイル - 1 つだけの出力ファイルが作成されます。 テキスト ファイルは書き込まれません。 ただし、サイズがゼロの .txt ファイルが作成されます。これにより、以前に、デバッガーによって書き込まれたテキスト ログが上書きでした。

出力ファイルは常にデスクトップの LogExts サブディレクトリに配置されます。この場所を変更することはできません。

デバッガーと Logexts.dll ロガーを実行している場合、これらの制限は適用されません。

 

 





