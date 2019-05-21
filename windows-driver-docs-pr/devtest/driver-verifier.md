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
ms.openlocfilehash: 47de964f7acb1ed8414626d0fc9e663c6e67f7b4
ms.sourcegitcommit: e3cf7d69c13846f3e7ece2b6178ecec23b9854ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2019
ms.locfileid: "65940376"
---
# <a name="driver-verifier"></a>ドライバーの検証ツール

Driver Verifier は、Windows カーネル モード ドライバーと無効な関数呼び出しまたはシステムが破損する可能性がありますアクションを検出するグラフィック ドライバーを監視します。 Driver Verifier は、負荷と不適切な動作を検索するテストのさまざまな Windows ドライバーをサブジェクトことができます。 負荷の大きい負荷、またはより多くの合理化されたテストを通じて、ドライバーを配置することができますが、実行するテストを構成できます。 実行することも Driver Verifier 複数のドライバーで同時に、または 1 つのドライバーで一度にします。

> [!Caution]
> <ul><li>Driver Verifier を実行している、コンピューターがクラッシュする可能性があります。</li>
> <li>Driver Verifier は、テストとデバッグを使用しているコンピューターでのみ実行する必要があります。</li>
> <li>Driver Verifier を使用するコンピューターの Administrators グループにする必要があります。</li>
> <li>Driver Verifier は、Windows 10 でのドライバーの動作の代わりにテストをお勧めします。 Windows 10 S には含まれません。</li></ul>


## <a name="where-can-i-download-driver-verifier"></a>Driver Verifier はどこでダウンロードできますか。

Verifier.exe として %WinDir%\system32\ に Windows のほとんどのバージョンに付属していますので、ドライバーの検証ツールをダウンロードする必要はありません。 (ドライバーの検証ツールは Windows 10 s. 含まれていません)Driver Verifier は、ダウンロード パッケージとして個別に配布されません。

ドライバー検証ツールの Windows 10 および Windows の以前のバージョンの変更については、次を参照してください<a href="driver-verifier--what-s-new.md" data-raw-source="[Driver Verifier: What's New](driver-verifier--what-s-new.md)">Driver Verifier:。新機能については</a>します。


## <a name="when-to-use-driver-verifier"></a>Driver Verifier を使用する場合

ドライバーの開発とテスト全体で Driver Verifier を実行します。 具体的には、次の目的の Driver Verifier を使用します。

-   修正するコストが簡単になり、開発サイクルの早い段階で問題が見つかりません。

-   トラブルシューティングとデバッグ テストに失敗し、コンピューターがクラッシュします。

-   動作の監視、WDK や、Visual Studio からテストを使用してテストするためのドライバーを展開するときに、 [Windows ハードウェア ラボ キット](https://go.microsoft.com/fwlink/p/?linkid=254893)(Windows HLK) または[Windows ハードウェア認定キット](https://docs.microsoft.com/en-us/previous-versions/windows/hardware/hck/jj124227(v=vs.85))(Windows 用8.1 の場合)。 ドライバーのテストの詳細については、次を参照してください。[ドライバーのテスト](https://docs.microsoft.com/en-us/windows-hardware/drivers/develop/testing-a-driver)します。


## <a name="how-to-start-driver-verifier"></a>Driver Verifier を開始する方法

テスト コンピューター、またはテストおよびデバッグしているコンピューター上にのみ、ドライバーの検証ツールを実行する必要があります。 Driver Verifier からを最大限に活用を取得するには、カーネル デバッガーを使用し、テスト コンピューターに接続する必要があります。 デバッグ ツールの詳細については、次を参照してください。[デバッグ ツールの Windows (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/index)します。

1. 開始、**コマンド プロンプト**ウィンドウを選択して**管理者として実行**、および種類**verifier**を開く**ドライバー検証マネージャー**。

2. 選択**標準設定を作成**(既定のタスク) をクリック**次**。

   選択することもできます**カスタム設定を作成する**定義済みの設定からを選択するか、個々 のオプションを選択します。 詳細については、次を参照してください。 [Driver Verifier のオプションとルール クラス](driver-verifier-options.md)と[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

3. **ことを確認するには、どのようなドライバーを選択**、次の表で説明されている選択方式のいずれかを選択します。

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
   <td align="left"><p>テストに役立つを必要としない Windows のバージョンを実行しているコンピューターでドライバーを署名します。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>以前のバージョンの Windows 向けに構築されたドライバーを自動的に選択します。</strong></td>
   <td align="left"><p>新しいバージョンの Windows でドライバーの互換性をテストするために便利です。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>このコンピューターにインストールされているすべてのドライバーを自動的に選択します</strong></td>
   <td align="left"><p>システムではテストされているドライバーの数の観点から最大のカバレッジを提供します。 このオプションは、ドライバーが他のデバイスや、システムにドライバーを操作できますテスト シナリオに便利です。</p>
   <p>このオプションは使用可能なリソースを使い果たすことができますも<a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a>といくつかのリソースを追跡します。 すべてのドライバーをテストするとシステムのパフォーマンスに悪影響を受けることができます。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>一覧からドライバー名を選択します。</strong></td>
   <td align="left"><p>ほとんどの場合、テストするには、どのドライバーを指定するされます。</p>
   <p>デバイス スタックのすべてのドライバーを選択すると、 <a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">I/O の検証の強化された</a>オプション オブジェクトを管理および各値が高いため、スタック内のドライバーの間で I/O 要求パケット (IRP) が渡されるために、コンプライアンスをチェックするにはエラーの検出時に提供される詳細レベル。</p>
   <p>システムまたはドライバーのパフォーマンス メトリックを測定するテスト シナリオを実行している場合、またはメモリの破損またはリソースの追跡の問題を検出するために使用可能なリソースの最大数を割り当てる場合は、1 つのドライバーを選択します (デッドロックなど、またはミュー テックス)。 <a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a>と<a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">I/O の検証</a>オプションは、一度に 1 つのドライバーを使用すると効果的です。</p></td>
   </tr>
   </tbody>
   </table>


4. 選択した場合**ドライバー名を一覧から選択**、 をクリックして**次**、し 1 つまたは複数の特定のドライバーを選択します。

5. をクリックして**完了**、コンピューターを再起動します。



>[!Note]
> ドライバー検証マネージャーを起動せず、コマンド プロンプト ウィンドウで Driver Verifier を実行することもできます。 たとえば、ドライバーで標準の設定をドライバーの検証を実行するという*myDriver.sys*は次のコマンドを使用します。
> ```console
> verifier /standard /driver myDriver.sys
> ```
>
> コマンド ライン オプションの詳細については、次を参照してください。 [ **Driver Verifier のコマンド構文**](verifier-command-line.md)します。



## <a name="how-to-control-driver-verifier"></a>Driver Verifier を制御する方法

ドライバー検証マネージャーまたは Driver Verifier を制御するコマンドラインのいずれかを使用することができます。 ドライバー検証マネージャーを開始するを参照してください。 [Driver Verifier を開始する方法](https://docs.microsoft.com/en-us/windows-hardware/drivers/devtest/driver-verifier#how-to-start-driver-verifier)、このトピックの「以前のバージョン。

次の操作ごとに、ドライバー検証マネージャーを使用して、またはコマンドラインを入力できます。


**停止、または Driver Verifier をリセットするには**

1. **ドライバー検証マネージャー**を選択します**既存の設定を削除**、 をクリックし、**完了**します。

    または

    コマンド プロンプトで次のコマンドを入力します。

    ```console
    verifier /reset
    ```

2. コンピューターを再起動します。


**Driver Verifier の統計を表示するには**

- **ドライバー検証マネージャー**を選択します**現在検証済みのドライバーに関する情報を表示**、順にクリックします**次**します。 クリックし続ける**次**追加情報が表示されます。

  または

  コマンド プロンプトで次のコマンドを入力します。

  ```console
  verifier /query
  ```


**Driver Verifier の設定を表示するには**

- **ドライバー検証マネージャー**を選択します**既存の設定を表示**、 をクリックし、**次**。

  または

  コマンド プロンプトで次のコマンドを入力します。

  ```console
  verifier /querysettings
  ```


## <a name="how-to-debug-driver-verifier-violations"></a>Driver Verifier の違反をデバッグする方法

最も大きなメリット Driver Verifier からを取得するには、カーネル デバッガーを使用し、テスト コンピューターに接続する必要があります。 Windows 用デバッグ ツールの概要については、次を参照してください。[デバッグ ツールの Windows (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/index)します。

Driver Verifier に違反が検出される場合は、コンピューターを停止させるバグ チェックが生成されます。 これは、問題をデバッグ可能なほとんどの情報を提供します。 ドライバーの検証を実行しているテスト コンピューターに接続されているカーネル デバッガーがあり、Driver Verifier 違反が検出されると、Windows はデバッガーを中断し、エラーの簡単な説明を表示します。

バグ チェックでドライバーの検証結果によって検出されたすべての違反。 一般的なバグの確認コードを以下に示します。

-   [**バグ チェック 0xC1 の。特別な\_プール\_検出\_メモリ\_破損**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc1--special-pool-detected-memory-corruption)
-   [**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)
-   [**バグ チェック 0xC6 の。ドライバー\_例外が発生しました\_変更\_FREED\_プール**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc6--driver-caught-modifying-freed-pool)
-   [**バグ チェック 0xC9 の。ドライバー\_VERIFIER\_IOMANAGER\_違反**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)
-   [**バグのチェックように。ドライバー\_ページ\_フォールト\_を超えて\_エンド\_の\_割り当て**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xd6--driver-page-fault-beyond-end-of-allocation)
-   [**バグ チェック 0xE6 の。ドライバー\_VERIFIER\_DMA\_違反**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/bug-check-0xe6--driver-verifier-dma-violation)

詳細については、次を参照してください。[をバグ チェック時にドライバーの検証ツールの処理が有効になっている](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/handling-a-bug-check-when-driver-verifier-is-enabled)します。 バグ チェック 0xC4 のデバッグに関するヒントについては、次を参照してください[デバッグ バグ チェック 0xC4:。ドライバー\_VERIFIER\_検出\_違反](debugging-bug-check-0xc4--driver-verifier-detected-violation.md)します。

新しいデバッグ セッションを開始するときに、デバッガー拡張機能のコマンドを使用して、 [ **! 分析**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-analyze)します。 カーネル モードで、 **! 分析**コマンドは、最新のバグ チェックに関する情報を表示します。 表示する*追加*については、エラーが発生したドライバーを識別できるように、追加オプション **-v**でコマンドを**kd >** プロンプト。

```dbgcmd
kd> !analyze -v
```

ほかに **! 分析**に、次のデバッガー拡張機能を入力することができます、 **kd >** Driver Verifier に固有の情報を表示するプロンプト。

-   [**! verifier** ](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-verifier)ダンプは、Driver Verifier の統計情報をキャプチャします。 使用 **! verifier のでしょうか。** すべての利用可能なオプションを表示します。

    ```dbgcmd
    kd> !verifier
    ```

-   [**! デッドロック**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-deadlock)ロックに関連する情報または Driver Verifier のデッドロック検出機能によって追跡されるオブジェクトが表示されます。 使用 **。 デッドロックのでしょうか。** すべての利用可能なオプションを表示します。

    ```dbgcmd
    kd> !deadlock
    ```

-   [**! iovirp** ](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-iovirp) \[*アドレス*\] I/O の検証ツールによって追跡 IRP に関連する情報が表示されます。 例:

    ```dbgcmd
    kd> !iovirp 947cef68
    ```

-   [**! ruleinfo** ](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-ruleinfo) \[ *RuleID* \]に関連する情報が表示されます、 [DDI 準拠の検査](ddi-compliance-checking.md)に違反していたルール。 (*RuleID*バグ チェックの最初の引数は、常にします)。DDI 準拠の 0x200 フォームでチェックからすべてのルール Id*nn*します。 例:

    ```dbgcmd
    kd> !ruleinfo 0x20005
    ```


## <a name="related-topics"></a>関連トピック

[Driver Verifier:新機能](driver-verifier--what-s-new.md)

[Driver Verifier のオプション](driver-verifier-options.md)

[**Driver Verifier のコマンド構文**](verifier-command-line.md)

[Driver Verifier を使用します。](using-driver-verifier.md)

[Driver Verifier を制御します。](controlling-driver-verifier.md)
