---
title: ドライバーの検証ツール
description: Driver Verifier は、Windows カーネル モード ドライバーと無効な関数呼び出しまたはシステムが破損する可能性がありますアクションを検出するグラフィック ドライバーを監視します。
ms.assetid: a8a78dde-930f-4d0b-be46-f7d07b0bf21b
keywords:
- ドライバー WDK、Driver Verifier の確認
- ドライバーの検証 WDK、Driver Verifier
- Driver Verifier WDK
- Driver Verifier WDK、Driver Verifier について
- 無効な関数呼び出しの WDK Driver Verifier
- ストレス テストを WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b42c6cdc01d3903c0f1bfd52174e92081ebaf9d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349769"
---
# <a name="driver-verifier"></a>ドライバーの検証ツール


Driver Verifier は、Windows カーネル モード ドライバーと無効な関数呼び出しまたはシステムが破損する可能性がありますアクションを検出するグラフィック ドライバーを監視します。 Driver Verifier は、負荷と不適切な動作を検索するテストのさまざまな Windows ドライバーをサブジェクトことができます。

行うことができます Driver Verifier 複数のドライバーで同時に、または 1 つのドライバーで一度にします。 負荷の大きい負荷、またはより多くの合理化されたテストを通じて、ドライバーを配置することができますが、実行するテストを構成できます。

-   [Driver Verifier はどこでダウンロードできますか。](#where-can-i-download-driver-verifier)
-   [Driver Verifier を使用する場合](#when-to-use-driver-verifier)
-   [Driver Verifier を開始する方法](#how-to-start-driver-verifier)
-   [Driver Verifier を制御する方法](#how-to-control-driver-verifier)
-   [Driver Verifier の違反をデバッグする方法](#how-to-debug-driver-verifier-violations)
-   [関連トピック](#related-topics)



## <a name="where-can-i-download-driver-verifier"></a>Driver Verifier はどこでダウンロードできますか。


<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 2000、Windows 10 s. を除き後で Windows のすべてのバージョンに含まれる、Driver Verifier (Verifier.exe) をダウンロードする必要はありません。個別のドライバーの検証ツールのダウンロード パッケージがない、%windir%\system32 ディレクトリ内にあります。 </p>
<ul>
<li>開く、<strong>コマンド プロンプト</strong>ウィンドウ (<strong>管理者として実行</strong>)。</li>
<li>型<strong>verifier</strong>ドライバー検証ツール マネージャーを開くまたは型<strong>verifier/でしょうか。</strong> コマンド ライン オプションを表示します。 参照してください<a href="verifier-command-line.md" data-raw-source="[&lt;strong&gt;Driver Verifier Command Syntax&lt;/strong&gt;](verifier-command-line.md)"> <strong>Driver Verifier のコマンド構文</strong></a>詳細についてはします。</li>
</ul>
<p></p>
<div class="alert">
<strong>注意</strong><br/><ul>
<li>Driver Verifier を実行している、コンピューターがクラッシュする可能性があります。</li>
<li>Driver Verifier は、テストとデバッグを使用しているコンピューターでのみ実行する必要があります。</li>
<li>Driver Verifier を使用するコンピューターの Administrators グループにする必要があります。</li>
<li>Windows 10 s. でドライバーの検証ツールが含まれていません。代わりに、Windows 10 でのドライバーの動作をテストすることをお勧めします。</li>
</ul>
</div>
<div>

</div>
<p>ドライバーのバージョンの Windows 8.1 と Windows の以前のバージョンの変更については、次を参照してください<a href="driver-verifier--what-s-new.md" data-raw-source="[Driver Verifier: What's New](driver-verifier--what-s-new.md)">Driver Verifier:。新機能については</a>します。</p></td>
</tr>
</tbody>
</table>





## <a name="when-to-use-driver-verifier"></a>Driver Verifier を使用する場合


ドライバーの開発全体で Driver Verifier を実行し、プロセスをテストします。

-   Driver Verifier を使用すると、修正するのにコストがときに簡単になり、開発ライフ サイクルの早い段階で問題を検索できます。

-   WDK、Visual Studio を使用したテスト用のドライバーを展開するときに、Driver Verifier を使用して、 [Windows ハードウェア認定キット](https://go.microsoft.com/fwlink/p/?linkid=254893)(HCK) テストします。 参照してください[ドライバーのテスト](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)します。

-   トラブルシューティングとテストの失敗やコンピューターのクラッシュをデバッグするのには、Driver Verifier を使用します。



## <a name="how-to-start-driver-verifier"></a>Driver Verifier を開始する方法


Driver Verifier は、テスト コンピューター、またはテストとデバッグのコンピューターでのみ実行する必要があります。 Driver Verifier からを最大限に活用を取得するには、カーネル デバッガーを使用し、テスト コンピューターに接続する必要があります。 参照してください[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)します。

1. 開く、**コマンド プロンプト**ウィンドウ (**管理者として実行**) と種類**verifier**ドライバー検証マネージャーを開きます。
2. 選択**標準設定を作成**(既定値) をクリック**次**。

   選択することもできます**カスタム設定を作成する**定義済みの設定からを選択するか、個々 のオプションを選択します。 参照してください[ドライバーの検証オプション](driver-verifier-options.md)と[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)詳細についてはします。

3. ドライバーまたは検証するドライバーを選択します。

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">オプション</th>
   <th align="left">推奨される使用</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>署名されていないドライバーを自動的に選択します</strong></td>
   <td align="left"><p>署名されたドライバーを必要としない Windows のバージョンを実行するコンピューターでテストするための便利なオプションです。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>以前のバージョンの Windows 向けに構築されたドライバーを自動的に選択します。</strong></td>
   <td align="left"><p>新しいバージョンの Windows でドライバーの互換性をテストするための便利なオプションです。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>このコンピューターにインストールされているすべてのドライバーを自動的に選択します</strong></td>
   <td align="left"><p>システムではテストされているドライバーの数の観点から最大のカバレッジを提供します。 このオプションは、ドライバーが他のデバイスや、システムにドライバーを操作できますテスト シナリオに便利です。</p>
   <p>このオプションは使用可能なリソースを使い果たすことができますも<a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a>といくつかのリソースを追跡します。 すべてのドライバーをテストするとシステムのパフォーマンスに悪影響を受けることができます。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>一覧からドライバー名を選択します。</strong></td>
   <td align="left"><p>ほとんどの場合、テストするには、どのドライバーを指定するされます。</p>
   <p>デバイス スタックのすべてのドライバーを選択すると、 <a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">I/O の検証の強化された</a>オブジェクトを追跡し、コンプライアンスを確認するように IRP スタック内のドライバーの間で渡されより詳細なレベルを指定するのには、オプションエラーを検出する必要があります。</p>
   <p>システムまたはドライバーのパフォーマンス メトリックを測定するテスト シナリオを実行している場合、またはメモリの破損またはリソースの追跡の問題 (デッドロック、mutexs) を検出するために使用可能なリソースの最大数を割り当てる場合は、1 つのドライバーを選択します。 <a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a>と<a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O の検証</a>オプションは、一度に 1 つのドライバーを使用すると効果的になります。</p></td>
   </tr>
   </tbody>
   </table>



4. クリックして**完了**し、コンピューターを再起動します。

**注**コマンド プロンプト ウィンドウで、Driver Verifier を実行することもできます。 たとえば、標準の設定で myDriver.sys と呼ばれるドライバーの Driver Verifier を実行するには、次のコマンドを使用します。



```
verifier  /standard /driver myDriver.sys
```

参照してください[ **Driver Verifier のコマンド構文**](verifier-command-line.md)詳細についてはします。



## <a name="how-to-control-driver-verifier"></a>Driver Verifier を制御する方法


**停止、または Driver Verifier をリセットするには**

1.  開く、**コマンド プロンプト**ウィンドウ (**管理者として実行**) と種類**verifier**ドライバー検証マネージャーを開きます。
2.  選択**既存の設定を削除**します。
3.  コンピューターを再起動します。

または、コマンド プロンプト ウィンドウで次のコマンドを入力し、コンピューターを再起動します。

```
verifier  /reset
```

**Driver Verifier の設定を表示するには**

1.  開く、**コマンド プロンプト**ウィンドウ (**管理者として実行**) と種類**verifier**ドライバー検証マネージャーを開きます。
2.  選択**既存の設定を表示**します。

または、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

```
verifier  /querysettings
```

**Driver Verifier の統計を表示するには**

1.  開く、**コマンド プロンプト**ウィンドウ (**管理者として実行**) と種類**verifier**ドライバー検証マネージャーを開きます。
2.  選択**現在検証済みのドライバーに関する情報を表示**します。

または、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

```
verifier  /query
```



## <a name="how-to-debug-driver-verifier-violations"></a>Driver Verifier の違反をデバッグする方法


Driver Verifier からを最大限に活用を取得するには、カーネル デバッガーを使用し、テスト コンピューターに接続する必要があります。 参照してください[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)詳細についてはします。

Driver Verifier に違反が検出される場合は、コンピューターを停止させるバグ チェックが生成されます。 これは、問題をデバッグ可能なほとんどの情報を提供します。 Driver Verifier 違反が検出される場合は、ドライバーの検証を実行するテスト コンピューターに接続されているカーネル デバッガーを使用すると、Windows はデバッガーを中断し、エラーの簡単な説明を表示します。

バグ チェックで、最も一般的な結果を (ただし、必ずしもそれらのすべて) に違反するすべての Driver Verifier は次のとおりです。

-   [**バグ チェック 0xC1 の。特別な\_プール\_検出\_メモリ\_破損**](https://msdn.microsoft.com/library/windows/hardware/ff560183)
-   [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)
-   [**バグ チェック 0xC6 の。ドライバー\_例外が発生しました\_変更\_FREED\_プール**](https://msdn.microsoft.com/library/windows/hardware/ff560193)
-   [**バグ チェック 0xC9 の。ドライバー\_VERIFIER\_IOMANAGER\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560205)
-   [**バグのチェックように。ドライバー\_ページ\_フォールト\_を超えて\_エンド\_の\_割り当て**](https://msdn.microsoft.com/library/windows/hardware/ff560267)
-   [**バグ チェック 0xE6 の。ドライバー\_VERIFIER\_DMA\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560341)

詳細については、[をバグ チェック時にドライバーの検証ツールの処理が有効になっている](https://msdn.microsoft.com/library/windows/hardware/hh450984)を参照してください。 バグ チェック 0xC4 のデバッグに関するヒントについては、次を参照してください[デバッグ バグ チェック 0xC4:。ドライバー\_VERIFIER\_検出\_違反](debugging-bug-check-0xc4--driver-verifier-detected-violation.md)します。

新しいデバッグ セッションを開始するときに、デバッガーの拡張機能のコマンドを使用して[ **! 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)します。 カーネル モードで、 **! 分析**コマンドは、最新のバグ チェックに関する情報を表示します。 **! 分析-v**コマンドは、追加情報が表示され、エラーが発生したドライバーを特定しようとしています。

```
kd> !analyze -v
```

さらに[ **! 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)、次のデバッガー拡張機能を使用して、Driver Verifier に固有の情報を表示することができます。

-   [**! verifier** ](https://msdn.microsoft.com/library/windows/hardware/ff565591)ダンプは、Driver Verifier の統計情報をキャプチャします。 使用 **! verifier のでしょうか。** すべての利用可能なオプションを表示します。

    ```
    kd> !verifier
    ```

-   [**! デッドロック**](https://msdn.microsoft.com/library/windows/hardware/ff562326)ロックに関連する情報または Driver Verifier のデッドロック検出機能によって追跡されるオブジェクトが表示されます。 使用 **。 デッドロックのでしょうか。** すべての利用可能なオプションを表示します。

    ```
    kd> !deadlock
    ```

-   [**! iovirp** ](https://msdn.microsoft.com/library/windows/hardware/ff563252) \[*アドレス*\] I/O の検証ツールによって追跡 IRP に関連する情報が表示されます。 以下に例を示します。

    ```
    kd> !iovirp 947cef68
    ```

-   [**! ruleinfo** ](https://msdn.microsoft.com/library/windows/hardware/dn265374) \[ *RuleID* \]に関連する情報が表示されます、 [DDI 準拠の検査](ddi-compliance-checking.md)に違反していたルール (*RuleID*バグ チェックの最初の引数は、常にします。 すべて DDI 準拠の検査*RuleID*フォーム 0x200nn に)。 例:

    ```
    kd> !ruleinfo 0x20005
    ```



## <a name="related-topics"></a>関連トピック


[Driver Verifier:新機能](driver-verifier--what-s-new.md)

[Driver Verifier のオプション](driver-verifier-options.md)

[**Driver Verifier のコマンド構文**](verifier-command-line.md)

[Driver Verifier を使用します。](using-driver-verifier.md)

[Driver Verifier を制御します。](controlling-driver-verifier.md)










