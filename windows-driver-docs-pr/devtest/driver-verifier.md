---
title: ドライバーの検証ツール
description: ドライバーの検証ツールは、Windows カーネルモードドライバーとグラフィックスドライバーを監視して、無効な関数呼び出しやシステムを破損する可能性があるアクションを検出します。
ms.assetid: a8a78dde-930f-4d0b-be46-f7d07b0bf21b
keywords:
- ドライバーの検証、ドライバーの検証
- ドライバー検証 WDK、ドライバー検証ツール
- ドライバー検証ツール WDK
- Driver Verifier WDK、Driver Verifier について
- 無効な関数呼び出し WDK Driver Verifier
- WDK Driver Verifier のストレステスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b881bd0657f7694e792636538b4371aaf23b51cb
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74860799"
---
# <a name="driver-verifier"></a>ドライバーの検証ツール

ドライバーの検証ツールは、Windows カーネルモードドライバーとグラフィックスドライバーを監視して、無効な関数呼び出しやシステムを破損する可能性があるアクションを検出します。 ドライバーの検証ツールは、Windows ドライバーにさまざまなストレスを適用し、不適切な動作を検出するためのテストを行います。 実行するテストを構成できます。これにより、高負荷の負荷によってドライバーを配置したり、より効率的なテストを行ったりすることができます。 また、複数のドライバーで同時に、または一度に1つのドライバーに対して、ドライバーの検証ツールを実行することもできます。

> [!Caution]
> <ul><li>ドライバーの検証ツールを実行すると、コンピューターがクラッシュする可能性があります。</li>
> <li>ドライバーの検証は、テストとデバッグに使用しているコンピューターでのみ実行してください。</li>
> <li>ドライバーの検証ツールを使用するには、コンピューターの Administrators グループにいる必要があります。</li>
> <li>Driver Verifier は Windows 10 S には含まれていないため、代わりに Windows 10 でドライバーの動作をテストすることをお勧めします。</li></ul>


## <a name="where-can-i-download-driver-verifier"></a>ドライバーの検証ツールはどこでダウンロードできますか。

%WinDir%\system32\ では、ほとんどのバージョンの Windows に含まれているため、ドライバーの検証ツールをダウンロードする必要はありません。 (Driver Verifier は Windows 10 S には含まれていません)。ドライバーの検証ツールは、ダウンロードパッケージとして個別に配布されません。

Windows 10 および windows の以前のバージョンでの Driver Verifier の変更については、「 <a href="driver-verifier--what-s-new.md" data-raw-source="[Driver Verifier: What's New](driver-verifier--what-s-new.md)">Driver verifier: 新機能</a>」を参照してください。


## <a name="when-to-use-driver-verifier"></a>ドライバーの検証ツールを使用する場合

ドライバーの開発とテストを通じて、ドライバーの検証ツールを実行します。 具体的には、次の目的でドライバーの検証ツールを使用します。

-   開発サイクルの早い段階で問題を見つけるために、より簡単で費用がかからない場合は、問題を解決します。

-   テストの失敗とコンピューターのクラッシュのトラブルシューティングとデバッグに使用します。

-   WDK、Visual Studio、および[Windows Hardware Lab kit](https://go.microsoft.com/fwlink/p/?linkid=254893) (windows HLK) または[Windows ハードウェア認定キット](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))(Windows 8.1) のテストを使用してテスト用のドライバーをデプロイするときの動作を監視する。 ドライバーのテストの詳細については、「[ドライバーのテスト](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)」を参照してください。


## <a name="how-to-start-driver-verifier"></a>ドライバーの検証ツールを開始する方法

ドライバー検証は、テストコンピューター、またはテストおよびデバッグしているコンピューターでのみ実行する必要があります。 ドライバーの検証ツールの利点を最大限に活用するには、カーネルデバッガーを使用して、テストコンピューターに接続する必要があります。 デバッグツールの詳細については、「 [Windows 用デバッグツール (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

1. **[管理者として実行]** を選択して**コマンドプロンプト**ウィンドウを起動し、「 **verifier** 」と入力して、**ドライバー検証マネージャー**を開きます。

2. **[標準設定の作成]** (既定のタスク) を選択し、 **[次へ]** をクリックします。

   **[カスタム設定の作成]** を選択して、定義済みの設定から選択することも、個々のオプションを選択することもできます。 詳細については、「 [Driver verifier options and rule classes](driver-verifier-options.md) 」と「 [driver verifier options](selecting-driver-verifier-options.md)」を参照してください。

3. **[確認するドライバーを選択してください]** で、次の表に記載されているいずれかの選択方式を選択します。

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">オプション</th>
   <th align="left">推奨される用途</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>署名されていないドライバーを自動的に選択する</strong></td>
   <td align="left"><p>署名されたドライバーを必要としない Windows のバージョンを実行しているコンピューターでのテストに役立ちます。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>以前のバージョンの Windows 用にビルドされたドライバーを自動的に選択する</strong></td>
   <td align="left"><p>新しいバージョンの Windows とドライバーの互換性をテストする場合に便利です。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>このコンピューターにインストールされているすべてのドライバーを自動的に選択する</strong></td>
   <td align="left"><p>システムでテストされているドライバーの数に関して最大カバレッジを提供します。 このオプションは、ドライバーがシステム上の他のデバイスまたはドライバーと対話できるテストシナリオに便利です。</p>
   <p>このオプションを使用すると、特別な<a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">プール</a>および一部のリソース追跡で利用可能なリソースを枯渇させることもできます。 すべてのドライバーをテストすると、システムのパフォーマンスに悪影響を及ぼすこともあります。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>一覧からドライバー名を選択する</strong></td>
   <td align="left"><p>ほとんどの場合、テストするドライバーを指定する必要があります。</p>
   <p>デバイススタック内のすべてのドライバーを選択すると、<a href="enhanced-i-o-verification.md" data-raw-source="[Enhanced I/O Verification](enhanced-i-o-verification.md)">拡張 I/o 検証</a>オプションを使用してオブジェクトを追跡し、対応を確認できます。これは、i/o 要求パケット (IRP) がスタック内の各ドライバー間で渡されるためです。これにより、エラーが検出された場合により詳細なレベルの詳細を提供できます。</p>
   <p>システムまたはドライバーのパフォーマンスメトリックを測定するテストシナリオを実行している場合や、メモリ破損またはリソース追跡の問題 (デッドロックなど) を検出するために使用できるリソースの最大数を割り当てる場合は、1つのドライバーを選択します。mutex)。 <a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特別なプール</a>および<a href="i-o-verification.md" data-raw-source="[I/O Verification](i-o-verification.md)">i/o 検証</a>オプションは、一度に1つのドライバーで使用するとより効果的です。</p></td>
   </tr>
   </tbody>
   </table>


4. **[一覧からドライバー名を選択]** する を選択した場合は、 **[次へ]** をクリックし、1つまたは複数の特定のドライバーを選択します。

5. **[完了]** をクリックし、コンピューターを再起動します。



>[!Note]
> ドライバー検証ツールマネージャーを起動せずに、コマンドプロンプトウィンドウでドライバーの検証ツールを実行することもできます。 たとえば、 *Mydriver*というドライバーで標準設定を使用して driver Verifier を実行するには、次のコマンドを使用します。
> ```console
> verifier /standard /driver myDriver.sys
> ```
>
> コマンドラインオプションの詳細については、「 [**Driver Verifier コマンド構文**](verifier-command-line.md)」を参照してください。



## <a name="how-to-control-driver-verifier"></a>ドライバーの検証機能を制御する方法

ドライバー検証ツールマネージャーまたはコマンドラインを使用して、ドライバーの検証機能を制御できます。 ドライバー検証マネージャーを起動するには、このトピックの前半の「[ドライバーの検証を開始する方法](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier#how-to-start-driver-verifier)」を参照してください。

次の各操作について、ドライバー検証マネージャーを使用するか、コマンドラインを入力できます。


**ドライバーの検証ツールを停止またはリセットするには**

1. **ドライバー検証マネージャー**で、 **[既存の設定を削除]** する を選択し、 **[完了]** をクリックします。

    または

    コマンド プロンプトに次のコマンドを入力します。

    ```console
    verifier /reset
    ```

2. コンピューターを再起動します。


**ドライバーの検証の統計情報を表示するには**

- **ドライバー検証マネージャー**で、 **[現在検証されているドライバーに関する情報を表示する]** を選択し、 **[次へ]** をクリックします。 **[次へ]** をクリックすると、追加情報が表示されます。

  または

  コマンド プロンプトに次のコマンドを入力します。

  ```console
  verifier /query
  ```


**ドライバーの検証の設定を表示するには**

- **ドライバー検証マネージャー**で、 **[既存の設定を表示]** する を選択し、 **[次へ]** をクリックします。

  または

  コマンド プロンプトに次のコマンドを入力します。

  ```console
  verifier /querysettings
  ```


## <a name="how-to-debug-driver-verifier-violations"></a>ドライバーの検証違反をデバッグする方法

Driver Verifier の利点を最大限に活用するには、カーネルデバッガーを使用して、テストコンピューターに接続する必要があります。 Windows 用デバッグツールの概要については、「 [windows 用デバッグツール (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

ドライバーの検証ツールによって違反が検出された場合、コンピューターを停止するバグチェックが生成されます。 これは、問題のデバッグに使用できる最も多くの情報を提供するためです。 ドライバーの検証ツールを実行しているテストコンピューターにカーネルデバッガーが接続されていて、ドライバーの検証ツールによって違反が検出された場合、Windows はデバッガーにブレークし、エラーの簡単な説明を表示します。

ドライバーの検証ツールによって検出されたすべての違反は、バグチェックになります。 一般的なバグチェックコードには、次のものがあります。

-   [**バグチェック 0xC1: 特別な\_プール\_検出されたメモリ\_破損\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc1--special-pool-detected-memory-corruption)
-   [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)
-   [**バグチェック 0xC6:\_解放された\_プールの変更\_ドライバー\_キャッチされました**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc6--driver-caught-modifying-freed-pool)
-   [**バグチェック 0xC9: ドライバー\_VERIFIER\_IOMANAGER\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc9--driver-verifier-iomanager-violation)
-   [**バグチェック 0xD6: ドライバー\_ページ\_フォールト\_\_割り当ての\_終了\_を超えています**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xd6--driver-page-fault-beyond-end-of-allocation)
-   [**バグチェック 0xE6: ドライバー\_VERIFIER\_DMA\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xe6--driver-verifier-dma-violation)

詳細については、「[ドライバーの検証機能が有効になっている場合のバグチェックの処理](https://docs.microsoft.com/windows-hardware/drivers/debugger/handling-a-bug-check-when-driver-verifier-is-enabled)」を参照してください。 バグチェックのデバッグに関するヒントについては、「[バグチェックのデバッグ 0xc4: ドライバー\_VERIFIER\_検出された\_違反](debugging-bug-check-0xc4--driver-verifier-detected-violation.md)」を参照してください。

新しいデバッグセッションを開始するときは、デバッガー拡張機能コマンドである[ **! analyze**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)を使用します。 カーネルモードでは、 **[分析]** コマンドを使用すると、最新のバグチェックに関する情報が表示されます。 *追加*情報を表示するには、エラーが発生したドライバーを識別するために、次のようにオプション **-v**を**kd >** プロンプトでコマンドに追加します。

```dbgcmd
kd> !analyze -v
```

**! Analyze**に加えて、次のデバッガー拡張機能を**kd >** プロンプトに入力して、Driver Verifier に固有の情報を表示できます。

-   [ **! verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)は、キャプチャされたドライバーの検証ツールの統計情報をダンプします。 **! Verifier-?** を使用します。 を選択すると、使用可能なすべてのオプションが表示されます。

    ```dbgcmd
    kd> !verifier
    ```

-   [ **! デッド**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-deadlock)ロックは、ドライバー検証ツールのデッドロック検出機能によって追跡されるロックまたはオブジェクトに関連する情報を表示します。 **! デッドロックを使用しますか?** を選択すると、使用可能なすべてのオプションが表示されます。

    ```dbgcmd
    kd> !deadlock
    ```

-   [ **! Ioブランコ p**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-iovirp) \[*アドレス*\] は、i/o 検証ツールによって追跡される IRP に関連する情報を表示します。 次に、例を示します。

    ```dbgcmd
    kd> !iovirp 947cef68
    ```

-   [ **! ruleinfo**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ruleinfo) \[*RuleID*\] に違反した[DDI 準拠チェック](ddi-compliance-checking.md)規則に関連する情報が表示されます。 (*RuleID*は常にバグチェックの最初の引数です)。DDI 準拠チェックからのすべての規則 Id は、0x200*nn*という形式になっています。 次に、例を示します。

    ```dbgcmd
    kd> !ruleinfo 0x20005
    ```


## <a name="related-topics"></a>関連トピック

[ドライバーの検証ツール: 新機能](driver-verifier--what-s-new.md)

[ドライバーの検証ツールのオプション](driver-verifier-options.md)

[**Driver Verifier コマンドの構文**](verifier-command-line.md)

[ドライバーの検証ツールの使用](using-driver-verifier.md)

[ドライバーの検証機能の制御](controlling-driver-verifier.md)
