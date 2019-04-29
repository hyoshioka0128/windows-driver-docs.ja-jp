---
title: 体系的な低リソースのシミュレーション
description: 体系的な低リソース シミュレーション オプションは、カーネル モード ドライバーにリソース エラーを挿入します。
ms.assetid: A8351715-8407-4FEF-9050-2F1F2E7FC2FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c11500c180357cff2c74e6aba614a6bbcc8d55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391302"
---
# <a name="systematic-low-resources-simulation"></a>体系的な低リソースのシミュレーション


体系的な低リソース シミュレーション オプションは、カーネル モード ドライバーにリソース エラーを挿入します。 このオプションは侵入ドライバー エラーのパスを処理します。 これらのパスをテスト歴史的非常に困難です。 体系的な低リソース シミュレーション オプションは、検出した再現可能な問題により、予測可能な方法でリソースの障害を挿入します。 エラー パスは、簡単に再現できますであるためにも簡単にこれらの問題の修正を確認します。

エラーの根本原因を特定するために、デバッガーの拡張機能は、挿入されているどのエラー正確に知ることができ、どのような順序で。

**注意**  すべてを確認する場合に、このオプションは使用想定していません (または、多数の) コンピューター上のドライバーです。 個々 のドライバーまたは接続されているフィルター ドライバーの対象となるテストを実行する場合にのみ、このオプションを使用する必要があります。 予測の結果になると同時に多数のドライバーでは、このオプションを使用してとをテストするドライバーに関係のないコンポーネントでの force クラッシュの可能性があります。

 

**注**  、Windows 8.1 用、[スタック ベースのエラー挿入](stack-based-failure-injection.md)Driver Verifier に、WDK 8 で利用できますが、機能が統合されました。 Windows 8.1 を実行するコンピューターでは、体系的な低リソース シミュレーションのオプションを使用します。

 

特定のドライバーに対して、体系的な低リソース シミュレーション オプションが有効の場合、カーネルと Ndis.sys には、ドライバーから一部の呼び出しを受け取ります。 体系的な低リソース シミュレーションが呼び出し履歴を調べ、具体的には、有効にするか、ドライバーに由来する呼び出しスタックの一部でします。 そのスタックを見たことも、初めての場合は、その呼び出しのセマンティクスに従って呼び出しは失敗します。 それ以外の場合、前に呼び出すことが示された場合、手を加えずを通過にされます。 体系的な低リソース シミュレーションには、ドライバーのロードし、複数回をアンロードするという事実を処理するロジックが含まれています。 呼び出し履歴が同じである場合でも、別のメモリ位置に、ドライバーが再読み込みが認識されます。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーの体系的な低リソース シミュレーション機能をアクティブ化することができます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。 アクティブ化または体系的な低リソース シミュレーションのオプションを非アクティブ化するコンピューターを再起動する必要があります。

-   **コマンドラインで**

    によって表される体系的な低リソース シミュレーション、コマンドラインで**verifier/flags 0x040000** (ビット 18)。 体系的な低リソース シミュレーション、0x040000 のフラグの値を使用してか 0x040000 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x040000 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    使用することができます、体系的な低リソース シミュレーション オプションを有効にすると、 **/faultssystematic** *オプション*コマンド ライン オプションをさらに体系的な低リソース シミュレーションを制御します。

    <table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">オプション</th>
    <th align="left">説明</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>enableboottime</p></td>
    <td align="left"><p>有効では、コンピューターの再起動後にインジェクションをフォールトします。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>disableboottime</p></td>
    <td align="left"><p>無効にします (これは既定の設定) コンピューターの再起動後にインジェクションを障害。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>recordboottime</p></td>
    <td align="left"><p>によりフォールト インジェクションで<em>what-if</em>モードにコンピューターを再起動します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>resetboottime</p></td>
    <td align="left"><p>コンピューターの再起動後に、フォールト インジェクションを無効にし、スタックの除外リストをクリアします。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>enableruntime</p></td>
    <td align="left"><p>フォールト インジェクションを動的に有効です。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>disableruntime</p></td>
    <td align="left"><p>フォールト インジェクションを動的に無効にします。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>recordruntime</p></td>
    <td align="left"><p>動的に有効の障害でインジェクション<em>what-if</em>モード。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>resetruntime</p></td>
    <td align="left"><p>動的にフォールト インジェクションを無効にし、以前にエラーが発生したスタックの一覧をクリアします。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>querystatistics</p></td>
    <td align="left"><p>フォールト インジェクションの現在の統計情報を示します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>incrementcounter</p></td>
    <td align="left"><p>単位テストは、障害が挿入されたときに識別するために使用するカウンターを渡します。</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>getstackid<em>カウンター</em></p></td>
    <td align="left"><p>識別子のスタックを取得しますが、指定された挿入します。</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>excludestack<em>超えて</em></p></td>
    <td align="left"><p>フォールト インジェクションからのスタックを除外します。</p></td>
    </tr>
    </tbody>
    </table>

     

-   **ドライバー検証マネージャーを使用します。**

    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック)**体系的な低リソース シミュレーション**します。
    5.  コンピューターを再起動します。

## <a name="span-iddebuggingbugcheckscausedbysystematiclowresourcessimulationspanspan-iddebuggingbugcheckscausedbysystematiclowresourcessimulationspanspan-iddebuggingbugcheckscausedbysystematiclowresourcessimulationspandebugging-bug-checks-caused-by-systematic-low-resources-simulation"></a><span id="Debugging_bug_checks_caused_by_Systematic_low_resources_simulation"></span><span id="debugging_bug_checks_caused_by_systematic_low_resources_simulation"></span><span id="DEBUGGING_BUG_CHECKS_CAUSED_BY_SYSTEMATIC_LOW_RESOURCES_SIMULATION"></span>体系的な低リソース シミュレーションによるデバッグのバグ チェック


ほとんどのバグで体系的な低リソース シミュレーションの結果で見つかった問題を確認します。 これらのコードのバグの原因を判断するため、 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)ツールの Windows 8.1 の拡張機能 (kdexts.dll) と必要なシンボルにデバッガーを提供します。

**デバッガーの拡張機能を実行するには**

-   デバッガーのコマンド プロンプトから次のコマンドを入力します。

    ```
    !verifier 0x800
    ```

これは、デバッガーが挿入され、最新の障害からの呼び出し履歴を表示する情報がダンプされます。

 

 





