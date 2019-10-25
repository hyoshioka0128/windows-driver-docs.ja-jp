---
title: Windows ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用
description: 静的ドライバー検証ツール (SDV) は、一連のインターフェイス規則とオペレーティングシステムのモデルを使用して、ドライバーが Windows オペレーティングシステムと正しく通信するかどうかを判断します。
ms.assetid: 94D4104C-66ED-4C1E-8EE1-4C669EB4EAAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb364809b2669f5fa6ae21b7af0e134f2d6d9f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839989"
---
# <a name="using-static-driver-verifier-to-find-defects-in-windows-drivers"></a>Windows ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用


静的ドライバー検証ツール (SDV) は、一連のインターフェイス規則とオペレーティングシステムのモデルを使用して、ドライバーが Windows オペレーティングシステムと正しく通信するかどうかを判断します。 SDV は、ドライバーの潜在的なバグを指している可能性のあるドライバーコードの欠陥を検出します。

SDV は、WDM、KMDF、NDIS、または Storport のいずれかのドライバーモデルに準拠するカーネルモードドライバーを分析できます。 詳細については、「[サポートされ](supported-drivers.md)ているドライバー」を参照し、「[静的ドライバーの検証ツールでドライバーまたはライブラリをサポートする](determining-if-static-driver-verifier-supports-your-driver-or-library.md)かどうかを判断する  さらに、SDV では、上記のドライバーモデルに準拠していないドライバーに対して、制限付きサポート (null の逆参照などの一般的なエラーに重点を置いた規則セット) が提供されます。

### <span id="preparing_your_source_code"></span><span id="PREPARING_YOUR_SOURCE_CODE"></span>

| ソースコードの準備 |
|----------------------------|
|                            |

分析用にコードを準備するには、次の手順に従います。

1.  **関数ロール型を使用してドライバーで提供される関数を宣言する**

    SDV では、関数ロール型宣言を使用して関数を宣言する必要があります。 たとえば、 [*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンは、ドライバー\_INITIALIZE 関数のロールの種類を使用して宣言する必要があります。

    ```
    DRIVER_INITIALIZE DriverEntry;
    ```

    宣言の後に、次のようにコールバックルーチンを実装 (または定義) します。

    ```
    /
    // Driver initialization routine
    //
    NTSTATUS 
      DriverEntry( 
        _In_ struct _DRIVER_OBJECT  *DriverObject,
        _In_ PUNICODE_STRING  RegistryPath 
        )
      {
          // Function body
      }
    ```

    サポートされている各ドライバーモデルには、ドライバーのコールバック関数とディスパッチルーチンに対する一連の関数ロールの種類があります。 これらの関数のロール型は、WDK ヘッダーファイルで宣言されています。 たとえば、次の関数プロトタイプは、Wdm に表示されているように、役割の種類を初期化するドライバー\_初期化されています。

    ```
    /
    // Define driver initialization routine type.
    //
    _Function_class_(DRIVER_INITIALIZE)
    _IRQL_requires_same_
    typedef
    NTSTATUS
    DRIVER_INITIALIZE (
        _In_ struct _DRIVER_OBJECT *DriverObject,
        _In_ PUNICODE_STRING RegistryPath
        );

    typedef DRIVER_INITIALIZE *PDRIVER_INITIALIZE;
    ```

    関数ロールの型は既に WDK ヘッダーファイルで定義されているため、コールバック関数をその型で宣言するだけで済みます。 この場合は、 *Driverentry*を type **DRIVER\_INITIALIZE**に宣言します。 ドライバーモデルの関数ロールの種類の完全な一覧については、「[関数ロール型宣言の使用](using-function-role-type-declarations.md)」を参照してください。

2.  **C/のコード分析の実行C++**

    ソースコードが準備されているかどうかを判断するために、Visual Studio で[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)を実行します。 コード分析ツールは、SDV が必要とする関数ロール型の宣言を確認します。 コード分析ツールを使用すると、失敗した可能性のある関数宣言を識別したり、関数定義のパラメーターが関数ロール型のパラメーターと一致しない場合に警告したりすることができます。

    -   Visual Studio でドライバープロジェクトを開きます。
    -   **[ビルド]** メニューの **[ソリューションでコード分析を実行]** をクリックします。

    結果は **[コード分析]** ウィンドウに表示されます。 失敗した可能性のある関数宣言を修正します。 また、コード分析ツールを構成して、ソリューションをビルドするたびに実行されるようにすることもできます。

    次の表は、コード分析ツールがドライバーコードで検出する可能性のある警告の一部を示しています。 静的ドライバー検証ツールを実行するには、ドライバーがこれらの欠陥を解放する必要があります。

    | C/C++ Warning のコード分析 | 説明                                                                                                                         |
    |---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
    | C28101                          | Drivers モジュールは、現在の関数が &lt;関数型&gt; 関数であることを推定しました。                                       |
    | C28022                          | この関数の関数クラスは、定義に使用された typedef の関数クラスと一致しません。                       |
    | C28023                          | 割り当てられている、または渡される関数には、少なくとも1つのクラスのクラス\_ 注釈\_\_関数が必要です                |
    | C28024                          | 割り当てられている関数ポインターには、function クラスで注釈が付けられています。関数クラスは、関数クラスのリストに含まれていません。 |
    | C28169                          | ディスパッチ関数 &lt;関数&gt; に \_ディスパッチ\_型\_ 注釈がありません                                             |
    | C28208                          | 関数シグネチャが関数宣言と一致しません                                                                     |



### <span id="running_static_driver_verifier"></span><span id="RUNNING_STATIC_DRIVER_VERIFIER"></span>

| 静的ドライバー検証ツールの実行 |
|--------------------------------|
|                                |

1.  Visual Studio でドライバープロジェクト (.Vcxproj) ファイルを開きます。 **[ドライバー]** メニューの **[静的ドライバー検証ツールの起動]** をクリックします。

    静的ドライバー検証アプリケーションが開きます。このアプリケーションでは、静的ドライバー検証ツールが分析を実行するタイミングを制御、構成、およびスケジュールできます。

2.  ドライバーにライブラリが含まれている場合は、 **[ライブラリ]** タブをクリックし、 **[ライブラリの追加]** をクリックしてライブラリを追加します。

    ライブラリのソースコードのディレクトリを参照し、プロジェクトファイル (.Vcxproj) を選択します。 ドライバーに含まれるすべてのライブラリを追加します。 SDV によってドライバーが分析される前に、ライブラリを追加する必要があります。 ドライバーの分析を開始すると、SDV によって、処理されていないライブラリも分析されます。 処理されたライブラリは、グローバル SDV キャッシュに格納されます。 詳細については、「[静的ドライバーの検証ツールでのライブラリの処理](library-processing-in-static-driver-verifier.md)」を参照してください。

3.  静的ドライバー検証ツールの構成設定を確認します。 **[構成]** タブをクリックします。

    **プロジェクトの構成**プロジェクト構成には、Visual Studio で選択した構成とプラットフォームの設定が表示されます。

    **リソース**ほとんどの場合、既定の設定を使用できます。 SDV がタイムアウト、停止、またはスペースを報告する場合は、これらの設定を調整してみてください。 詳細については、「[静的ドライバーの検証のトラブルシューティングに関する推奨事項](recommendations-for-troubleshooting-static-driver-verifier.md)」を参照してください。

    **スケジュール**確認を開始する開始時刻を選択します。 既定の設定では、**メイン**タブの **[開始]** をクリックした直後に分析が開始されます。ドライバーのサイズと複雑さによっては、静的な分析の実行に時間がかかることがあります。 分析が最も便利なときに開始するようにスケジュールすることもできます。たとえば、一日の終わりにあります。

    **メモ** コンピューターの電源管理計画を確認して、分析中にコンピューターがスリープ状態にならないようにしてください。



4.  **[ルール]** タブをクリックして、分析の開始時に検証するドライバ API 使用ルールを選択します。

    静的ドライバー検証ツールは、分析しているドライバーの種類 (WDF、WDM、NDIS、または Storport) を検出し、ドライバーの種類の既定の規則セットを選択します。 ドライバーで SDV を初めて実行する場合は、既定の規則セットを実行する必要があります。

    規則の詳細については、「 [DDI コンプライアンス規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

5.  スタティック分析を開始します。 **[メイン]** タブをクリックし、 **[開始]** をクリックします。 **[開始]** をクリックすると、静的分析がスケジュールされていて、分析の実行に時間がかかる可能性があることを知らせるメッセージが表示されます。 [OK] をクリックして続行します。 分析は、スケジュールした時点から開始されます。

### <span id="viewing_and_analyzing_the_results"></span><span id="VIEWING_AND_ANALYZING_THE_RESULTS"></span>

| 結果の表示と分析 |
|-----------------------------------|
|                                   |

静的分析が続行されると、SDV によって分析の状態がレポートされます。 分析が完了すると、SDV によって結果と統計情報が報告されます。 ドライバーが API の使用規則を満たしていない場合、結果は欠陥として報告されます。

問題が発生した場合は、SDV によって**警告**ページと**エラー**ページに問題が表示されます。 **[ドライバーのプロパティ]** ページには、特定のドライバーのプロパティに対するテストの結果が表示されます。 ドライバーのプロパティのテストは、分析をさらに限定するドライバーの機能を識別するために使用されます。 ドライバーの**プロパティ**の結果を使用して、ドライバーの必要なプロパティとサポートされている機能を確認できます。

[静的ドライバーの検証ツールレポート](static-driver-verifier-report.md)で特定の欠陥を表示するには、**結果**ウィンドウでその欠陥をクリックします。 [トレースビューアー](defect-viewer.md)が開き、ルール違反へのコードパスのトレースが表示されます。 詳細については、「[静的ドライバーの検証結果の解釈](interpreting-static-driver-verifier-results.md)」を参照してください。

**メモ** 静的ドライバー検証ツールは、分析の結果と設定を保持します。 結果を消去するには、 **[クリーン]** をクリックします。



### <a name="span-idtroubleshooting_sdv_resultsspanspan-idtroubleshooting_sdv_resultsspantroubleshooting-static-driver-verifier-results"></a><span id="troubleshooting_sdv_results"></span><span id="TROUBLESHOOTING_SDV_RESULTS"></span>静的ドライバーの検証結果のトラブルシューティング

SDV が問題が検出されなかったことを報告する場合は、 **[メイン]** タブで、エントリポイントが検出されていることを確認します。 関数ロールの種類を使用して関数を宣言していない場合、SDV はドライバーコードの欠陥を分析して検出することができません。 詳細については、「[関数ロール型宣言の使用](using-function-role-type-declarations.md)」を参照してください。

SDV がタイムアウトを報告したり、有用な結果を返すことができなかった場合は、一部の SDV 構成オプションを変更する必要がある場合があります。 SDV のトラブルシューティング方法の詳細については、「[静的ドライバーの検証のトラブルシューティングに関する推奨事項](recommendations-for-troubleshooting-static-driver-verifier.md)」を参照してください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[静的ドライバーの検証ツールでドライバーまたはライブラリがサポートされているかどうかを確認する](determining-if-static-driver-verifier-supports-your-driver-or-library.md)

[関数ロール型宣言の使用](using-function-role-type-declarations.md)

[静的ドライバーの検証規則](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)










