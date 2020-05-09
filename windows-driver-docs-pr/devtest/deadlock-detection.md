---
title: デッドロックの検出
description: デッドロックの検出
ms.assetid: ecda3e19-218d-484a-973d-8406bed8d820
keywords:
- デッドロック検出機能 WDK ドライバー検証ツール
- デッドロック WDK ドライバー検証ツール
- ロックされたリソース WDK ドライバーの検証ツール
- スレッドが WDK ドライバー検証ツールをロックする
ms.date: 07/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: de7979d72bdc6899b51b83eae388d51476b3a690
ms.sourcegitcommit: 076f9cd83313f6d8ab5688340f05bde7e8fbb8ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82999077"
---
# <a name="deadlock-detection"></a>デッドロックの検出


## <span id="ddk_deadlock_detection_tools"></span><span id="DDK_DEADLOCK_DETECTION_TOOLS"></span>


デッドロック検出は、ロックする必要があるリソース (スピンロック、ミューテックス、高速ミューテックス) をドライバーが使用しているかを監視します。 この Driver Verifier オプションは、将来のある時点でデッドロックを引き起こす可能性のあるコードロジックを検出します。

Driver Verifier のデッドロック検出オプションは、 **! デッドロック**カーネルデバッガー拡張機能と共に、コードがこれらのリソースの不適切な使用を回避するための効果的なツールです。

デッドロック検出は、Windows XP 以降のバージョンの Windows でのみサポートされています。


### <a name="span-idcauses_of_deadlocksspanspan-idcauses_of_deadlocksspancauses-of-deadlocks"></a><span id="causes_of_deadlocks"></span><span id="CAUSES_OF_DEADLOCKS"></span>デッドロックの原因

*デッドロック*は、複数のスレッドがいくつかのリソースを競合している場合に発生します。このような方法では実行できません。

最も一般的な形式のデッドロックは、2つ以上のスレッドが他のスレッドによって所有されているリソースを待機しているときに発生します。 次に例を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">スレッド1</th>
<th align="left">スレッド2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ロックを取得します。</p></td>
<td align="left"><p>ロック B を取得します</p></td>
</tr>
<tr class="even">
<td align="left"><p>ロック B を要求する</p></td>
<td align="left"><p>ロック A を要求する</p></td>
</tr>
</tbody>
</table>

 

両方のシーケンスが同時に発生した場合、スレッド1はスレッド2によって所有されているため、ロック B は取得されず、スレッド1が所有しているため、スレッド2はロックを取得しません。 これにより、関係するスレッドが停止し、最悪の場合、システムは応答を停止します。

デッドロックは、2つのスレッドと2つのリソースに限定されません。 3つのスレッドと3つのロックの間の3方向のデッドロックは一般的ですが、5部構成または6部構成のデッドロックが発生することもあります。 これらのデッドロックでは、同時に発生するさまざまな処理に依存しているため、"悪い運" が必要になることがあります。 ただし、ロックの取得がさらに離れているほど、これらがになる可能性が高くなります。

スレッドが既に所有しているロックを取得しようとすると、シングルスレッドのデッドロックが発生する可能性があります。

すべてのデッドロックの共通分母は、ロック階層が尊重されないことです。 一度に複数のロックを取得する必要がある場合は常に、各ロックに明確な優先順位を設定する必要があります。 A が B の前にあり、B の前に A がある場合、階層は A-B-C になります。 これは、B または C の後にを取得する必要がなく、C の後に B を取得する必要がないことを意味します。

デッドロックが発生する可能性がない場合でも、ロック階層に従う必要があります。コードを保持するプロセスでは、デッドロックが誤って発生することが簡単になるためです。

### <a name="span-idresources_that_can_cause_deadlocksspanspan-idresources_that_can_cause_deadlocksspanresources-that-can-cause-deadlocks"></a><span id="resources_that_can_cause_deadlocks"></span><span id="RESOURCES_THAT_CAN_CAUSE_DEADLOCKS"></span>デッドロックの原因となる可能性のあるリソース

最も明確なデッドロックは、*所有*しているリソースの結果です。 これには、スピンロック、ミューテックス、高速ミューテックス、および ERESOURCEs が含まれます。

(イベントや LPC ポートなどで) 取得されるのではなく、シグナル状態になっているリソースは、よりあいまいなデッドロックの原因となる傾向があります。 もちろん、これらのリソースは、2つのスレッドが完了するまで無期限に待機してしまうような方法で、コードによって誤用される可能性があります。 ただし、これらのリソースは実際には1つのスレッドによって所有されていないため、滞納スレッドを明確に区別することはできません。

ドライバー検証ツールのデッドロック検出オプションは、スピンロック、ミューテックス、および高速ミューテックスに関連する可能性のあるデッドロックを検索します。 ERESOURCEs の使用を監視したり、所有されていないリソースの使用を監視したりすることはありません。

### <a name="span-ideffects_of_deadlock_detectionspanspan-ideffects_of_deadlock_detectionspaneffects-of-deadlock-detection"></a><span id="effects_of_deadlock_detection"></span><span id="EFFECTS_OF_DEADLOCK_DETECTION"></span>デッドロック検出の影響

ドライバー検証ツールのデッドロック検出ルーチンは、必ずしも同時ではないロック階層違反を検出します。 ほとんどの場合、これらの違反は、確率が指定されるとデッドロックするコードパスを識別します。

潜在的なデッドロックを検出するために、ドライバー検証ツールはリソース取得順序のグラフを作成し、ループを確認します。 リソースごとに1つのノードを作成し、別のロックが取得されるたびに矢印を描画する場合、パスループはロック階層違反を表します。

これらの違反のいずれかが検出されると、ドライバーの検証ツールはバグチェックを発行します。 これは、実際のデッドロックが発生する前に発生します。

**ただし**   、競合するコードパスが同時に発生しない場合でも、ロック階層違反が含まれている場合は、コードパスを書き直す必要があります。 このようなコードは、コードが若干書き換えられた場合に、実際のデッドロックを引き起こす可能性がある "デッドロックの発生を待機しています" です。

 

デッドロック検出によって違反が検出されると、バグチェック0xC4 が発行されます。 このバグチェックの最初のパラメーターは、正確な違反を示します。 次のような違反が考えられます。

-   ロック階層違反に含まれる2つ以上のスレッド

-   シーケンスから解放されるリソース

-   同じリソースを2回取得しようとするスレッド (自己デッドロック)

-   最初に取得されずに解放されるリソース

-   取得したものとは異なるスレッドによって解放されたリソース

-   2回以上初期化されていないか、まったく初期化されていないリソース

-   リソースをまだ所有しているときに削除されるスレッド

-   Windows 7 以降では、ドライバーの検証ツールでデッドロックが発生する可能性があります。 たとえば、通常のスピンロックとスタックキューに\_格納されたスピンロックの両方として、同じ kspin lock データ構造体を使用しようとしているとします。


バグチェックパラメーターの一覧につい\_て\_は\_、「[**バグチェック 0xc4**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (ドライバー検証ツールが検出された違反)」を参照してください。

### <a name="span-idmonitoring_deadlock_detectionspanspan-idmonitoring_deadlock_detectionspanmonitoring-deadlock-detection"></a><span id="monitoring_deadlock_detection"></span><span id="MONITORING_DEADLOCK_DETECTION"></span>デッドロック検出の監視

デッドロック検出によって違反が検出されると、 **! デッドロック**カーネルデバッガー拡張機能を使用して、何が発生したかを正確に調べることができます。 ロック階層トポロジ、およびロックが最初に取得されたときの各スレッドの呼び出し履歴を表示できます。

[**! デッドロック**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-deadlock)拡張の詳細な例と、デバッガー拡張機能に関する一般的な情報については、「Windows 用デバッグツール」パッケージのドキュメントを参照してください。 詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証ツールマネージャーまたは Verifier コマンドラインを使用して、1つまたは複数のドライバーのデッドロック検出機能をアクティブにすることができます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

-   **コマンドラインで**

    コマンドラインでは、デッドロック検出オプションは**ビット 5 (0x20)** で表されます。 デッドロック検出をアクティブにするには、フラグ値0x20 を使用するか、フラグ値に0x20 を追加します。 次に例を示します。

    ```
    verifier /flags 0x20 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows Vista 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動しなくても、デッドロック検出をアクティブ化および非アクティブ化することができます。 次に例を示します。

    ```
    verifier /volatile /flags 0x20 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    デッドロック検出機能も、標準設定に含まれています。 次に例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  [**カスタム設定の作成] (コード開発者向け)** を選択し、[**次へ**] をクリックします。
    2.  [**完全な一覧から個々の設定を選択]** を選択します。
    3.  **デッドロック検出**を選択 (チェック) します。

    デッドロック検出機能も、標準設定に含まれています。 この機能を使用するには、ドライバー検証マネージャーで [**標準設定の作成**] をクリックします。

 

 





