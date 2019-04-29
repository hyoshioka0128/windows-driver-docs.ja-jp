---
title: 再起動します
description: 再起動します
ms.assetid: 8AB66CAB-9BAA-4911-A143-618627226B78
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02549bbc4e798526fdf37bf50ff97bb42084d6bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387443"
---
# <a name="reboot"></a>再起動します


TAEF により、テストのことが原因または、コンピューターを再起動する必要がありますを指定します。 機能は、2 ~ 3 つのコンポーネントで構成されますメタデータ可能性があります原因または TAEF、再起動を実行または間もなくテストが開始した再起動し、これらの操作を実行していることを選択するコマンド オプションの TAEF を通知することを要求するための API の再起動を必要とすると、テストにフラグを設定するには。ローカルで実行するときに、テストします。

## <a name="span-idbehaviorrebootspanspan-idbehaviorrebootspanbehavior"></a><span id="behavior_reboot"></span><span id="BEHAVIOR_REBOOT"></span>動作


コンピューターの再起動の特定のセマンティクスが必要になる TAEF 実行モデルや、保証をセットアップおよび後処理用の操作の成功と失敗の動作を変更するとします。

-   再起動の動作は、フィクスチャ (セットアップとクリーンアップ) が (適切なメタデータ) でテストできるだけです。
-   かどうか、再起動 API を使用から任意の場所、適切なマークアップを含むテスト以外、この関数は返されません。 代わりに、TAEF は、テスト プロセスを強制終了します。 このテストの作成方法と、テスト コードのバグを表しますを固定する必要があります。
-   テスト フィクスチャは、再起動の境界では実行されません。 つまり、(かどうか、テストは、再起動を開始します。 または、TAEF 自体、再起動が発生することを要求) 場合でも再起動前に破棄操作を実行しないと、再起動後にセットアップ操作は実行されません。
-   通知またはテストが完了するまで再起動を要求する時点からログ記録 (およびその結果のログのエラー) は無視されます。

## <a name="span-idmetadatarebootspanspan-idmetadatarebootspanmetadata"></a><span id="metadata_reboot"></span><span id="METADATA_REBOOT"></span>メタデータ


再起動の Api の使用を有効にするテストを設定してフラグ必要がある、 **RebootPossible**メタデータを **"true"** します。 クラスにすべてのテストは再起動する場合に、クラス レベルで指定することができます、このメタデータがメタデータの継承の通常の規則に従います (再起動するのではなく重量性質を指定された場合ことがテストについて明示的な決定を行うことをお勧めでき、再起動を開始することはできません)。 ドキュメントを参照して[C++ でのテストの作成](authoring-tests-in-c--.md)と[でテストを作成C#](authoring-tests-in-c-.md)メタデータの仕様の例についてはします。

## <a name="span-idapirebootspanspan-idapirebootspanapi"></a><span id="api_reboot"></span><span id="API_REBOOT"></span>API


コンピューターの再起動を処理するための 2 つのメイン関数があります。

-   **Reboot(Option)** TAEF にテスト マシンの再起動が開始される要求。
-   **RebootCustom(Option)** テストが、テスト コンピューターの再起動の原因となっているは TAEF を通知します。 この API には、システムのクラッシュもサポートしています。 TAEF は API が返された後に、該当するデータがフラッシュされたことを確認します。

**オプション**パラメーターが、再開の動作のいずれかを指定します。

-   **再実行**、原因で、再起動が発生した後にもう一度同じテストの実行に TAEF
-   **引き続き**、原因で、再起動が発生した後に、次のテストを実行する TAEF

### <a name="span-idnativerebootspanspan-idnativerebootspannative"></a><span id="native_reboot"></span><span id="NATIVE_REBOOT"></span>ネイティブ

Interruption.h ヘッダーをなどで、関数の呼び出しによって再起動 Api へのアクセス、 **WEX::TestExecution::Interruption**名前空間。 次の 4 つの可能な呼び出しは次のとおりです。

```cpp
using namespace WEX::TestExecution;
Interruption::Reboot(RebootOption::Rerun);
Interruption::Reboot(RebootOption::Continue);
Interruption::RebootCustom(RebootOption::Rerun);
Interruption::RebootCustom(RebootOption::Continue);
```

### <a name="span-idmanagedrebootspanspan-idmanagedrebootspanmanaged"></a><span id="managed_reboot"></span><span id="MANAGED_REBOOT"></span>管理されています。

2 つのメソッドのいずれかを呼び出し、**中断**静的クラスで、**かかえるします。TestExecution**内に置かれている名前空間**Te.Managed.dll**:

```cpp
using WEX.TestExecution;
Interruption.Reboot(RebootOption.Rerun);
Interruption.Reboot(RebootOption.Continue);
Interruption.RebootCustom(RebootOption.Rerun);
Interruption.RebootCustom(RebootOption.Continue);
```

## <a name="span-idpromptrebootspanspan-idpromptrebootspancommand-prompt-usage"></a><span id="prompt_reboot"></span><span id="PROMPT_REBOOT"></span>コマンド プロンプトを使用


この機能の最適な使用方法で再起動が可能性のある TAEF テストを実行する[クロス マシン実行](cross-machine-execution.md)または WTT によって。 このような場合 TAEF により再起動実行暗黙的に\*作業の流れを中断する必要がありますいないため、します。 ローカル コンピューターに手動で再起動するテストの実行は TAEF を使用してその状態をキャッシュする既定のパスをオーバーライドする必要があるか、明示的にテストの再起動にオプトインする必要があります。 そうでない場合、どのテストでも再起動としてマークされますブロックします。 ローカルで実行するときに、再起動のテストを有効にするするには、次のコマンド引数を使用します。

``` syntax
Te.exe /rebootStateFile:MyRestartFile.xml
```

TAEF の状態を格納する指定されたファイルが作成されます (テストが既にコンパイルされて実行すると、任意の TAEF コマンドまたは環境のオプションなど) し、再起動後に再開したときに箇所から再開します。 TAEF 処理自体が動作するコンピューターとを再実行して、再起動後にもう一度です。

このオプションは、(RunOnce キー) を再起動した後、テストを再開する TAEF が依存する機能が削除されるため、ARM マシンで動作しないことに注意してください。

\* 任意の互換性のない実行機能を使用していない限り、(現在[並列](parallel.md)と[テスト モード](test-modes.md))。

## <a name="span-idfaqsrebootspanspan-idfaqsrebootspanfrequently-asked-questions"></a><span id="faqs_reboot"></span><span id="FAQS_REBOOT"></span>よく寄せられる質問


### <a name="span-idrerunfaqspanspan-idrerunfaqspanif-i-choose-rerun-is-there-any-way-i-can-tell-whether-the-test-is-being-invoked-for-the-first-time-or-after-a-restart"></a><span id="rerun_faq"></span><span id="RERUN_FAQ"></span>再実行を選択した場合は、最初に、または再起動の後に、テストが呼び出されているかどうかを知ることができる方法ではありますか。

TAEF では、これを実現するための機能は提供されません。 再実行オプションの目的は、再起動が完了するまでは、Windows Update を実行している) など、マシンの状態に基づいての不確定の数を必要とするテストを記述するためです。 使用を検討して、 [ExecutionGroup](execution-groups.md)と続行のオプションをタスク シーケンスの前に、/後の再起動が発生する別のテストの操作に分割します。

### <a name="span-idothertestsfaqspanspan-idothertestsfaqspanwhich-taef-test-types-are-supported"></a><span id="othertests_faq"></span><span id="OTHERTESTS_FAQ"></span>どの TAEF テストの種類がサポートされますか。

この機能は、ネイティブに利用可能な管理、およびスクリプトをテストします。

 

 





