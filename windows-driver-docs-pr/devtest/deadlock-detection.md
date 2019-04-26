---
title: デッドロックの検出
description: デッドロックの検出
ms.assetid: ecda3e19-218d-484a-973d-8406bed8d820
keywords:
- デッドロック検出機能 WDK Driver Verifier
- デッドロック WDK Driver Verifier
- ロックされたリソース WDK Driver Verifier
- スレッドのロック WDK Driver Verifier
ms.date: 07/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: adaf103c38fe11afca2ce8cba65d7c98bc0bde92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344926"
---
# <a name="deadlock-detection"></a>デッドロックの検出


## <span id="ddk_deadlock_detection_tools"></span><span id="DDK_DEADLOCK_DETECTION_TOOLS"></span>


デッドロックの検出では、リソースをロックする--迅速に作成する必要があるロック、ミュー テックス、および高速なミュー テックスのドライバーの使用を監視します。 このドライバーの検証オプションでは、今後ある時点でデッドロックが発生する可能性があるコード ロジックを検出します。

ドライバーの検証ツールのデッドロック検出オプションと共に、 **! デッドロック**カーネル デバッガー拡張機能は有効なツールとこれらのリソースの不適切な使用を回避するので、コードを確認してください。

デッドロックの検出は、Windows XP および Windows の以降のバージョンでのみサポートされます。


### <a name="span-idcausesofdeadlocksspanspan-idcausesofdeadlocksspancauses-of-deadlocks"></a><span id="causes_of_deadlocks"></span><span id="CAUSES_OF_DEADLOCKS"></span>デッドロックの原因

A*デッドロック*が 2 つまたは複数のスレッドが実行することはできません、このような方法で、いくつかのリソースの競合に付属している場合に発生します。

最も一般的な形式のデッドロックは、2 つまたは複数のスレッドが他のスレッドによって所有されているリソースを待機しているときに発生します。 これは、次のように示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">スレッド 1</th>
<th align="left">スレッド 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ロック A</p></td>
<td align="left"><p>ロック B</p></td>
</tr>
<tr class="even">
<td align="left"><p>要求ロック B</p></td>
<td align="left"><p>要求ロック A</p></td>
</tr>
</tbody>
</table>

 

同時に両方のシーケンスする場合は、スレッド 1 られるロック B 2 のスレッドによって所有されていると、スレッド 2 は 1 のスレッドによって所有されているため、ロック A 取得しないためです。 停止すると、関連するスレッドの原因最高と最低 at により、システムは、応答を停止します。

デッドロックは、2 つのスレッドと 2 つのリソースに限定されません。 3 ウェイ デッドロックと 3 つのロックの 3 つのスレッド間では、共通--と 5 部構成または 6 部もデッドロックが生じる。 これらのデッドロックがある程度の「縁起が悪い」を必要と多くの同時に発生することに依存しているためです。 ただし、距離、ロックの取得は、可能性が高くようになります。

シングル スレッドのデッドロックは、スレッドが既に所有しているロックを取得しようとしたときに発生します。

すべてのデッドロックの間で共通分母は、ロック階層が守られていないことです。 を、一度に 1 つ以上のロックする必要があるたびに、各ロックは、クリアの優先順位が必要です。 階層に A から B、C が B の前に 1 つのポイントと B が C の前に別の A を実行するされた場合 つまり、C. 後 B または C、B を取得する必要がありますいない後しない必要がありますが獲得すること

ロック階層は、コードを保守するプロセスでは、デッドロックを誤って導入を簡単になりますので、デッドロックの可能性がない場合でも従う必要があります。

### <a name="span-idresourcesthatcancausedeadlocksspanspan-idresourcesthatcancausedeadlocksspanresources-that-can-cause-deadlocks"></a><span id="resources_that_can_cause_deadlocks"></span><span id="RESOURCES_THAT_CAN_CAUSE_DEADLOCKS"></span>デッドロックを引き起こす可能性のあるリソース

最も明確なデッドロックの結果である*所有*リソース。 これらには、スピン ロック、ミュー テックス、高速なミュー テックス、および ERESOURCEs が含まれます。

(イベントや LPC ポート) を取得するのではなく、シグナル状態にはリソースは、はるかにあいまいなデッドロックが発生する傾向があります。 可能であり、一般的すぎるではもちろん、このような方法でこれらのリソースを誤って使用するコードの相互を完了するまで無期限に待機する 2 つのスレッドが終了します。 ただし、これらのリソースが実際には、1 つのスレッドが所有していないためには、確実に滞納スレッドを識別することはできません。

Driver Verifier のデッドロック検出オプションは、スピン ロック、ミュー テックス、および高速なミュー テックスを伴う可能性のあるデッドロックを検索します。 ERESOURCEs の使用を監視しませんもは nonowned リソースの使用を監視します。

### <a name="span-ideffectsofdeadlockdetectionspanspan-ideffectsofdeadlockdetectionspaneffects-of-deadlock-detection"></a><span id="effects_of_deadlock_detection"></span><span id="EFFECTS_OF_DEADLOCK_DETECTION"></span>デッドロック検出の効果

Driver Verifier のデッドロックの検出ルーチンでは、必ずしも同時ではない階層違反ロックを検索します。 ほとんどの場合、これらの違反は、遷移時にデッドロックが発生するコード パスを特定します。

潜在的なデッドロックを見つけるには、Driver Verifier は、リソース取得順のグラフを構築し、for ループ チェックします。 リソースごとにノードを作成する前に、別の時間の 1 つのロックが取得される矢印を描画する場合は、パスのループはロック階層の違反を表します。

Driver Verifier はこれらの違反が検出されたときのバグ チェックを発行します。 これは、すべて実際のデッドロックが発生する前に発生します。

**注**  場合でも、競合するコード パスが同時に実行できることはありません、書き直す必要がまだありますロック階層の違反が含まれる場合。 このようなコードは、「デッドロックの発生を待機している」実際のデッドロックを引き起こす可能性、コードが多少記述し直す場合。

 

デッドロックの検出には、違反が検出されると、バグ チェック 0xC4 を発行します。 このバグ チェックの最初のパラメーターでは、正確な違反を示します。 違反は次のとおりです。

-   ロック階層の違反に関連する 2 つまたは複数のスレッド

-   シーケンスからリリースされているリソース

-   同じリソースは 2 回 (を自己デッドロック) を取得しようとするスレッド

-   最初に取得されていることなしにリリースされているリソース

-   取得したものとは異なるスレッドでリリースされているリソース

-   2 回以上初期化またはすべての初期化されていないリソース

-   リソースをまだ所有している削除されたスレッド

-   Windows 7 以降、Driver Verifier はデッドロックの可能性を予測できます。 たとえば、同じ KSPIN を使用しよう\_正規スピン ロックとスタックの両方のロックのデータ構造には、スピン ロックがキューに登録します。


参照してください[**バグ チェック 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (ドライバー\_VERIFIER\_検出\_違反)、バグの一覧については、パラメーターを確認します。

### <a name="span-idmonitoringdeadlockdetectionspanspan-idmonitoringdeadlockdetectionspanmonitoring-deadlock-detection"></a><span id="monitoring_deadlock_detection"></span><span id="MONITORING_DEADLOCK_DETECTION"></span>デッドロックの検出を監視します。

デッドロックの検出、違反を検出すると、 **! デッドロック**カーネル デバッガーの拡張機能を使用して何が発生した正確に調査できます。 ロックが取得された最初の時点で、ロック階層のトポロジと各スレッドの呼び出し履歴を表示できます。

最良の結果をドライバーの問題の上で実行される、Windows のチェック ビルドより完全な実行時のスタック トレースを取得するカーネルを利用できるためです。

詳細な例は、 [ **! デッドロック**](https://msdn.microsoft.com/library/windows/hardware/ff562326)拡張機能とツールを Windows のデバッグ パッケージ内のドキュメントで、デバッガーの拡張機能に関する一般的な情報。 参照してください[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)詳細についてはします。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバーのデッドロック検出機能をアクティブにできます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインで**

    、コマンドラインでは、デッドロックの検出 オプションで表される**ビット 5 (0x20)** します。 デッドロックの検出を有効にするには、0x20 のフラグの値を使用して、または 0x20 をフラグ値に追加します。 次に、例を示します。

    ```
    verifier /flags 0x20 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows Vista と Windows の以降のバージョンでもアクティブ化し、デッドロックの検出を追加することで、コンピューターを再起動しなくても非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x20 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

    デッドロック検出機能は、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    2.  選択**完全な一覧から個々 の設定を選択します。** します。
    3.  選択 (チェック)**デッドロックの検出**します。

    デッドロック検出機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

 

 





