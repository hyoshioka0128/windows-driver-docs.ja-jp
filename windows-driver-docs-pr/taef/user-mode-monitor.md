---
title: ユーザー モードのモニタ
description: ユーザー モードのモニタ
ms.assetid: CE6CEC2C-5E8E-40aa-A5D3-0062D6F82EFE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fbd12a98997fda7ecc2470aed5ba61ee3d27f1e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537625"
---
# <a name="user-mode-monitor"></a>ユーザー モードのモニタ


ユーザー モードのモニターにより、'プロセスでテスト' の実行に関する詳細なコンテキストを取得するためのテスト、テストの失敗を調査するため、または既存のテストからの向上の検証を有効にする詳細なコンテキストを取得するためにします。 現在のユーザー モードのモニターの実装では、詳細のカスタマイズと構成の後続のリリースで予定で、基本的な実装を提供します。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>概要


低レベルの Windows API は、特定のプロセス - から発信されるすべての 'デバッガー' イベントの通知のユーザー モード モニター (UMM) の使用は、スレッドの開始と停止、モジュールの読み込み、クラッシュ、し、少しだけ名前の例外を処理します。 デバッガー イベント、UMM を受信するとは、コードはコメントをログ記録 (テストに失敗した) するために、エラーをログ記録、テスト対象プロセスのミニダンプことなど、いくつかの操作のいずれかで実行できます。

## <a name="span-idenablingtheusermodemonitorspanspan-idenablingtheusermodemonitorspanspan-idenablingtheusermodemonitorspanenabling-the-user-mode-monitor"></a><span id="Enabling_the_User_Mode_Monitor"></span><span id="enabling_the_user_mode_monitor"></span><span id="ENABLING_THE_USER_MODE_MONITOR"></span>ユーザー モードのモニターを有効にします。


特定のテスト ケース UMM を有効にするには、構成の 2 つの情報を提供する必要があります。

1.  テストは、'ProcessUnderTest' メタデータの値でマークする必要があります。 これにより、テストされるプロジェクトのプロセスを識別する UMM できます。
2.  Te.exe コマンドラインを含める必要があります '/userModeMonitor' UMM 機能を有効にします。

UMM コードを使用する場合に、次の点を考慮する必要があります。

1.  名前付きプロセスでテストを実行している複数のインスタンスがある場合、インスタンスが、検出された最初に使用されます。
2.  テスト自動化を実行しているユーザーは、テスト対象のプロセスからデバッガー イベントを受信するための十分なアクセス許可が必要です。
3.  UMM コードは ' アタッチ' テスト対象のプロセスをすべてセットアップ フィクスチャが実行すると 'デタッチ' クリーンアップ フィクスチャを実行する前にします。 これにより、テストのセットアップのフィクスチャを、テストのプロセスを開始し、テストの準備に必要な初期化を実行できます。

## <a name="span-idsupportedusermodemonitoractionsspanspan-idsupportedusermodemonitoractionsspanspan-idsupportedusermodemonitoractionsspansupported-user-mode-monitor-actions"></a><span id="Supported_User_Mode_Monitor__Actions_"></span><span id="supported_user_mode_monitor__actions_"></span><span id="SUPPORTED_USER_MODE_MONITOR__ACTIONS_"></span>ユーザー モードのモニター"Actions"がサポートされています


ユーザー モードのモニターには、監視対象のプロセスで指定されたデバッガー イベントが発生したときにかかることが 'アクション' のセットがあります。 現在の実装では、特定のイベントだけ呼び出しの既定のアクション。現在の構成のサポートはありません。

| アクション     | 説明                                                            |
|------------|------------------------------------------------------------------------|
| LogComment | イベントからコンテキスト情報と共に、ログには、コメントを追加します。 |
| LogError   | 現在のテストが失敗すると、ログにエラーが記録されます。            |
| ミニダンプ   | ミニダンプを書き込み、ログに保存します。                         |
| 無視     | 何もしません。                                                          |

 

## <a name="span-idsupportedusermodemonitoreventsspanspan-idsupportedusermodemonitoreventsspanspan-idsupportedusermodemonitoreventsspansupported-user-mode-monitor-events"></a><span id="Supported_User_Mode_Monitor__Events_"></span><span id="supported_user_mode_monitor__events_"></span><span id="SUPPORTED_USER_MODE_MONITOR__EVENTS_"></span>'イベント' のユーザー モード モニターのサポート


ユーザー モードのモニターには、上、記載されている '操作' のいずれかに適用可能な ' イベント' が表示されます。 次の表では、現在の既定のイベントを受信したときに実行されるアクションと共に、報告されたイベントの一覧を示します。

| イベント                                | 既定のアクション (2 番目のチャンスの既定のアクション) |
|--------------------------------------|-----------------------------------------------|
| スレッドを作成します。                        | 無視                                        |
| スレッドを終了します。                          | 無視                                        |
| プロセスを作成します。                       | 無視                                        |
| プロセスを終了します。                         | LogError                                      |
| モジュールの読み込み                          | LogComment                                    |
| モジュールのアンロード                        | 無視                                        |
| システム エラー                         | 無視                                        |
| 最初のブレークポイント                   | LogError                                      |
| 初期のモジュールの読み込み                  | 無視                                        |
| デバッグ対象の出力                      | LogComment                                    |
| アクセス違反                     | LogError (LogError)                           |
| アサーション エラー                    | LogError (LogError)                           |
| アプリケーションのハング                     | LogError (LogError)                           |
| 中断命令例外          | LogError                                      |
| 中断命令の例外を続行します。 | 無視                                        |
| C++ EH 例外                     | LogError (LogError)                           |
| CLR 例外                        | LogError (LogError)                           |
| CLR 通知例外           | LogError (無視)                             |
| コントロール LogError 例外           | LogError                                      |
| コントロール LogError 例外を続行します。  | 無視                                        |
| コントロール C 例外                  | LogError                                      |
| コントロール C 例外を続行します。         | 無視                                        |
| データの不整合                      | LogError (LogError)                           |
| デバッガー コマンド例外           | 無視                                        |
| ガード ページ違反                 | LogError (LogError)                           |
| 無効な命令                  | LogError (LogError)                           |
| ページ I/O エラー                    | LogError (LogError)                           |
| 整数 0 による除算               | LogError (LogError)                           |
| 整数のオーバーフロー                     | LogError (LogError)                           |
| ハンドルが無効です。                       | LogError                                      |
| 無効なハンドルを続行します。              | LogError                                      |
| 無効なロックのシーケンス                | LogError (LogError)                           |
| 無効なシステムの呼び出し                  | LogError (LogError)                           |
| ポートの切断                    | LogError (LogError)                           |
| サービスの停止                         | LogError (LogError)                           |
| 1 つのステップの例外                | LogError                                      |
| 1 つのステップの例外を続行します。       | 無視                                        |
| スタック バッファー オーバーフロー                | LogError (LogError)                           |
| スタック オーバーフロー                       | LogError (LogError)                           |
| 検証の停止                        | LogError (LogError)                           |
| ビジュアルの C++ 例外                 | 無視 (無視)                               |
| デバッガーを起動します。                        | LogError (LogError)                           |
| WOW64 のブレークポイント                     | LogError (無視)                             |
| WOW64 の 1 つのステップの例外          | LogError (無視)                             |
| その他の例外                      | LogError (LogError)                           |

 

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


UMM 機能の使用を示すためには、するには 'MSPaint' を自動化するテストの (多少不自然な) 例を見てをみましょう。

```cpp
namespace UserModeMonitorExample
{
    using System;
    using System.Diagnostics;
    using System.Threading;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using WEX.Logging.Interop;
    using WEX.TestExecution;

    [TestClass]
    public class BasicExample
    {
        [TestInitialize]
        public void TestInitialize()
        {
            Process[] runningPaintInstances = Process.GetProcessesByName("mspaint.exe");

            Verify.IsTrue(runningPaintInstances.Length == 0, "There are no running instances of mspaint.exe");

            this.mspaintUnderTest = Process.Start("mspaint.exe");
        }

        [TestCleanup]
        public void TestCleanup()
        {
            // Close the &#39;mspaint under test&#39; - if it&#39;s already gone, this will throw, but that&#39;s no big deal.
            this.mspaintUnderTest.CloseMainWindow();
        }

        [TestMethod]
        [TestProperty("ProcessUnderTest", "mspaint.exe")]
        [TestProperty("Description", "Shows how a test can be failed if the UI is closed from underneath the test.")]
        public void SimpleInteraction()
        {
            Log.Comment("If the &#39;user mode monitor&#39; is enabled and mspaint.exe is closed,&quot;);
            Log.Comment(&quot;then this test will be failed.&quot;);
            Log.Comment("Sleeping for 5 seconds");

            Thread.Sleep(TimeSpan.FromSeconds(5));
        }

        private Process mspaintUnderTest;
    }
}
```

次に、テストの構造の簡単な内訳を示します。

-   'SimpleInteraction' テストは、UI ベースのアプリケーションと対話するテストを表します:"MSPaint.exe"をここでは、します。 このテストは"mspaint.exe"プロセスのテストを呼び出す"ProcessUnderTest"メタデータが適用されたことに注意してください。
-   テストは、セットアップ フィクスチャがあることを実行している既存のインスタンスがないとをテストする 1 つのインスタンスを起動することを確認します。
-   テストは、フィクスチャのセットアップで起動されたインスタンスを閉じるクリーンアップ フィクスチャがあります。

'Test' は非常に簡単です、考えられる結果を見てみましょう。

1.  問題なくテストが実行されます。 これは、最適な考えられる結果です。
2.  有効になっている UMM、なしは、ユーザーは、実行中に MSPaint インスタンスを閉じます。 ここで、テストは成功するが、クリーンアップは、'InvalidOperationException' で失敗します。
3.  UMM が有効になっているとは、ユーザーは、実行中に MSPaint インスタンスを閉じます。 ここでは、UMM コードでは、プロセスのテストが失敗に閉じられたことを示すエラーが表示がログに記録されます。 (2) の場合と同様、クリーンアップが失敗します。

有効になっている UMM、誤った動作は、すぐが報告され、テスト結果に直接影響します。 これは、可能であり、余分なコンテキストは、デバッグまたはテストのエラーについて支援を提供できるだけ早くエラーが報告されるため、パターンがはるかにもっと適切なテストです。

 

 





