---
title: Windows ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用
description: Static Driver Verifier (SDV) は、一連のインターフェイスのルールと、オペレーティング システムのモデルを使用して、Windows オペレーティング システムとドライバーが正しく対話するかどうかを決定します。
ms.assetid: 94D4104C-66ED-4C1E-8EE1-4C669EB4EAAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecf17c5836dd28eb12f398a4fb11bbf9c342a960
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574059"
---
# <a name="using-static-driver-verifier-to-find-defects-in-windows-drivers"></a>Windows ドライバーの不具合を見つけるための静的ドライバー検証ツールの使用


Static Driver Verifier (SDV) は、一連のインターフェイスのルールと、オペレーティング システムのモデルを使用して、Windows オペレーティング システムとドライバーが正しく対話するかどうかを決定します。 SDV は、ドライバーでの潜在的なバグを指すドライバー コードの欠陥を検出します。

SDV は、次のドライバー モデルのいずれかに準拠しているカーネル モード ドライバーを分析できます。WDM、KMDF、NDIS、または Storport します。 詳細については、次を参照してください。[ドライバーのサポートされている](supported-drivers.md)と[Static Driver Verifier に、ドライバーまたはライブラリがサポートしているかを決定する](determining-if-static-driver-verifier-supports-your-driver-or-library.md)します。  さらに、SDV は、上記のドライバー モデルに従っていないドライバーの (null などの一般的なエラーに重点を置いて厳しく制限されるルール セットを逆参照)、制限付きサポートを提供します。

### <span id="preparing_your_source_code"></span><span id="PREPARING_YOUR_SOURCE_CODE"></span>

| ソース コードを準備します。 |
|----------------------------|
|                            |

次の手順を使用すると、分析のため、コードを準備できます。

1.  **ロールの種類の関数を使用して、ドライバーによって提供される関数を宣言します。**

    SDV は、関数の役割の種類の宣言を使用して、関数を宣言することが必要です。 たとえば、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンは、ドライバーを使用して宣言する必要があります\_INITIALIZE 関数ロールの種類。

    ```
    DRIVER_INITIALIZE DriverEntry;
    ```

    宣言の後にする実装 (定義) 次のように、コールバック ルーチン。

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

    各ドライバーのサポートされているモデルでは、ドライバーのコールバック関数とディスパッチ ルーチンの関数のロールの種類のセットがあります。 これらの関数の役割の種類は、WDK のヘッダー ファイルで宣言されます。 たとえば、ドライバーの関数のプロトタイプをここでは\_Wdm.h にほど INITIALIZE ロールの種類が表示されます。

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

    関数のロールの種類は、WDK のヘッダー ファイルで既に定義されて、ため、のみ、その型に、コールバック関数を宣言する必要があります。 この場合を宣言する*DriverEntry*型**ドライバー\_初期化**します。 ドライバー モデルの関数のロールの種類の完全な一覧を参照してください。[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。

2.  **C/C++ のコード分析を実行します。**

    ソース コードを準備するかどうかを判断するために、実行、[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)Visual Studio でします。 Sdv は関数の役割型宣言に対するコード分析ツールを確認します。 コード分析ツールはできなかった可能性がありますを関数の宣言を特定できますまたは関数のロールの種類の関数定義のパラメーターが一致しない場合に警告を表示します。

    -   Visual Studio で、ドライバーのプロジェクトを開きます。
    -   **ビルド** メニューのをクリックして**ソリューションでコード分析を実行**します。

    結果が表示されます、**コード分析**ウィンドウ。 できなかった可能性がありますを関数の宣言を修正します。 ソリューションをビルドするたびに実行するようコード分析ツールを構成することもできます。

    次の表は、いくつかの警告をドライバー コードのコード分析ツールを探すことがあります。 Static Driver Verifier を実行するには、ドライバーはこれらの欠陥の必要があります。

    | C/C++ の警告のコード分析 | 説明                                                                                                                         |
    |---------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
    | C28101                          | Drivers モジュールは、現在の関数がある推論が、&lt;関数型&gt;関数                                       |
    | C28022                          | この関数の関数クラスでは、それを定義するために使用された typedef の関数クラスが一致しません。                       |
    | C28023                          | 割り当てられているされたり、渡された関数が必要、\_関数\_クラス\_クラスの少なくとも 1 つの注釈                |
    | C28024                          | 割り当てられる関数ポインターが関数クラスの一覧に含まれていないが関数クラスを使用して注釈を付けます。 |
    | C28169                          | ディスパッチ関数&lt;関数&gt;されていない\_ディスパッチ\_型\_注釈                                             |
    | C28208                          | 関数シグネチャ、関数宣言と一致しません                                                                     |



### <span id="running_static_driver_verifier"></span><span id="RUNNING_STATIC_DRIVER_VERIFIER"></span>

| Static Driver Verifier の実行 |
|--------------------------------|
|                                |

1.  Visual Studio で、ドライバーのプロジェクト (.vcxProj) ファイルを開きます。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

    これは、制御、構成、および Static Driver Verifier は、分析を実行するときにスケジュール設定をする、Static Driver Verifier アプリケーションを開きます。

2.  ドライバーには、ライブラリが含まれている場合にクリックして、**ライブラリ** タブでをクリックし、**ライブラリの追加**ライブラリを追加します。

    ライブラリのソース コードのディレクトリに移動し、プロジェクト ファイル (.vcxProj) を選択します。 すべてのドライバーを含むライブラリを追加します。 SDV は、ドライバーを分析する前に、ライブラリを追加する必要があります。 ドライバーの分析を開始するときに SDV も処理されていないライブラリを分析します。 ライブラリが処理された後は、グローバルの SDV のキャッシュに格納されます。 詳細については、次を参照してください[Static Driver Verifier でライブラリの処理。](library-processing-in-static-driver-verifier.md)

3.  Static Driver Verifier の構成設定を確認します。 **[構成]** タブをクリックします。

    **プロジェクトの構成**構成と Visual Studio で選択したプラットフォームの設定、プロジェクト構成を示しています。

    **リソース**ほとんどの場合、既定の設定を使用することができます。 SDV は、タイムアウト、停止、または Spaceout を報告する場合は、これらの設定を調整することを試してください可能性があります。 詳細については、次を参照してください。 [Static Driver Verifier のトラブルシューティングに関する推奨事項](recommendations-for-troubleshooting-static-driver-verifier.md)します。

    **スケジュール**を開始する検証の開始時刻を選択します。 既定の設定がクリックした後すぐに分析を開始するには**開始**上、 **Main**タブ。ドライバーとその複雑さのサイズによっては、静的分析の実行に長い時間がかかります。 分析できます。 最も便利なときに開始するスケジュールを設定します。たとえば、1 日の終わり。

    **注**をコンピュータに、コンピューターの電源管理プランは省きますスリープ状態の分析中に確認してください。



4.  をクリックして、**ルール**分析を開始することを確認するドライバー API の使用状況規則を選択するタブ。

    Static Driver Verifier の種類の検出のドライバー (WDF、WDM、NDIS、または Storport) を分析しているし、ドライバーの種類の既定の規則セットを選択します。 最初に、ドライバーでは、SDV を実行している場合は、既定の規則セットを実行する必要があります。

    ルールについては、次を参照してください。 [DDI 準拠規則](https://msdn.microsoft.com/library/windows/hardware/ff552840)します。

5.  静的分析を開始します。 をクリックして、 **Main**タブをクリックし、をクリックして**開始**します。 クリックすると**開始**分析が実行に長時間かかることやスタティック分析をスケジュールすることを知らせるメッセージが表示されます。 続行するには、 **[OK]** をクリックします。 分析は、スケジュールした時刻に開始します。

### <span id="viewing_and_analyzing_the_results"></span><span id="VIEWING_AND_ANALYZING_THE_RESULTS"></span>

| 表示して、結果の分析 |
|-----------------------------------|
|                                   |

静的分析の進行に伴って SDV は、分析の状態を報告します。 分析が完了したら、SDV は、結果と統計情報を報告します。 ドライバーは、API 使用量のルールを満たすために失敗した場合、結果は、障害として報告されます。

SDV ものの表示を上の問題が発生した場合、**警告**と**エラー**ページ。 **ドライバー プロパティ**ページには、特定のドライバーのプロパティのテストの結果が表示されます。 ドライバーのプロパティのテストは、分析をさらに修飾するドライバーの機能を識別するために使用されます。 使用することができます、**ドライバー プロパティ**結果が予期されるプロパティを確認して、ドライバーの機能をサポートします。

特定の障害を表示する、[静的ドライバー検証ツールのレポート](static-driver-verifier-report.md)の欠陥をクリックして、**結果**ウィンドウ。 開き、[トレース ビューアー](defect-viewer.md)、規則違反コード パスのトレースが表示されます。 詳細については、次を参照してください。[静的ドライバー検証結果を解釈する](interpreting-static-driver-verifier-results.md)します。

**注**Static Driver Verifier は、結果と分析から設定を保持します。 結果をクリアするには、クリックして**クリーン**します。



### <a name="span-idtroubleshootingsdvresultsspanspan-idtroubleshootingsdvresultsspantroubleshooting-static-driver-verifier-results"></a><span id="troubleshooting_sdv_results"></span><span id="TROUBLESHOOTING_SDV_RESULTS"></span>Static Driver Verifier の結果のトラブルシューティング

SDV は、欠陥が見つからなかったことを報告する場合は、確認、 **Main**  タブのエントリ ポイントが検出されたことを確認します。 ドライバーが関数のロールの種類を使用して関数を宣言しない場合は、SDV は分析し、ドライバーのコードの欠陥を検出することできません。 詳細については、次を参照してください。[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。

SDV は、タイムアウトを報告または有用な結果に失敗した場合は、いくつかの SDV の構成オプションを変更する必要があります。 SDV のトラブルシューティングを行う方法の詳細については、次を参照してください。 [Static Driver Verifier のトラブルシューティングに関する推奨事項](recommendations-for-troubleshooting-static-driver-verifier.md)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Static Driver Verifier に、ドライバーまたはライブラリがサポートしているかを決定します。](determining-if-static-driver-verifier-supports-your-driver-or-library.md)

[関数の役割の種類の宣言を使用してください。](using-function-role-type-declarations.md)

[Static Driver Verifier の規則](https://msdn.microsoft.com/library/windows/hardware/ff552840)

[コード分析ツール](https://go.microsoft.com/fwlink/p/?linkid=226836)










