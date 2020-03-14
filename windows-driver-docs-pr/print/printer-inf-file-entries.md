---
title: プリンター INF ファイル エントリ
description: プリンター INF ファイル エントリ
ms.assetid: 897072bb-e481-4c8d-a2bf-57b19c69ac0e
keywords:
- INF ファイル WDK print、エントリ
- 依存ファイル WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 812dff15cb58d8d0901c33a73cd6c9044c8bfbe1
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242947"
---
# <a name="printer-inf-file-entries"></a>プリンター INF ファイル エントリ





プリントサーバーにプリンターをインストールするインストールアプリケーションでは、スプーラの**Addprinter Driverex**関数を呼び出してドライバーファイルを読み込み、スプーラの**addprinter**関数を呼び出してプリンターをサーバーで使用できるようにする必要があります。

**Addprinter Driverex**関数では、入力として DRIVER\_info\_3 構造体が必要です。また、 **addprinter**関数では、入力として、プリンター\_情報\_2 の構造を必要とします。 既定の Windows 2000 以降のプリンタークラスインストーラー Ntprint.inf は、プリンターの INF ファイルを読み取って、関数が呼び出される前にこれらの構造体に配置する必要がある文字列値を取得します。


**Addprinter Driverex**および**addprinter**関数と、ドライバー\_INFO\_3 および PRINTER\_info\_2 の構造については、Microsoft Windows SDK のドキュメントを参照してください。

Ntprint.inf が認識するプリンタードライバーの一連の INF ファイルエントリが定義されています。 これらのエントリの形式は次のとおりです。

*EntryName* = *値*

ここで、 *EntryName*はエントリを識別する文字列であり、*値*はエントリに割り当てられた文字列値です。

次の表に、プリンターの INF ファイルに含める必要がある INF ファイルのエントリを示します。 各エントリについて、テーブルには次のものが含まれます。

-   エントリに割り当てられる値。

-   エントリが定義されていない場合に Ntprint.inf が使用する既定値。

-   Ntprint.inf がエントリ値へのポインターを配置する構造体メンバー。

| INF ファイルのエントリ       |値|既定値 (エントリが指定されていない場合)|構造体メンバー |
|----------------------|-----|-------------|-----------------------------------------|
| ConfigFile           | ドライバーの[プリンターインターフェイス DLL](printer-interface-dll.md)の名前。 | DriverFile に指定された値。 | ドライバー\_INFO\_3 構造の**pConfigFile**メンバー (Windows SDK のドキュメントを参照) |
| DataFile             | ドライバーに関連付けられたデータファイルの名前 (PPD ファイルなど)。 | INF ファイル内のドライバーのセクション名。 | ドライバー\_INFO\_3 構造体の**Pdatafile ファイル**メンバー |
| DefaultDataType      | NT ベースのオペレーティングシステムでは使用されません。 |||
| DriverCategory       | この表の後にある**注 1**を参照してください。 | INF ファイルでドライバーカテゴリが指定されていない場合 (ほとんどの v3 ドライバーと同様)、ドライバーのカテゴリが**Printfax. Printer**であることが前提となります。 | なし |
| DriverFile           | ドライバーの[プリンターグラフィックス DLL](printer-graphics-dll.md)の名前。 | INF ファイル内のドライバーのセクション名。 | **pDriverPath**のドライバー\_INFO\_3 構造体のメンバー |
| ExcludeFromSelect    | この表の後にある**注 2**を参照してください。 | なし | なし |
| HelpFile             | インターフェイス DLL のヘルプファイルの名前。 | [なし]。 ヘルプファイルが指定されていません。 | DRIVER\_INFO\_3 構造体の**Phelpfile**メンバー |
| LanguageMonitor      | プリンタドライバに関連付けられる言語モニタの名前。 「 **LanguageMonitor Value Format** 」セクションを参照してください。 | [なし]。 言語モニターが指定されていません。 | DRIVER\_INFO\_3 構造体の**Pmonitorname**メンバー |
| PrintProcessor       | プリンターキューに関連付けられるプリントプロセッサの名前。 「 **Printprocessor 値の形式**」セクションを参照してください。 | 既定のプリントプロセッサ (WinPrint) が使用されます。 | DRIVER\_INFO\_2 構造体の**Pprintprocessor**メンバー (Windows SDK のドキュメントを参照) |
| VendorSetup          | カスタマイズされた[プリンターセットアップ操作](customized-printer-setup-operations.md)を処理する、ベンダーが提供する DLL 内の関数の名前。 | [なし]。 次の表に従って、**メモ 3**を参照してください。 | なし |
| 受信トレイ Versionrequired | INF が参照するすべてのコアドライバーに対して許容される最小バージョン。 受信トレイ Versionrequired の詳細については、「 [INF の Versionrequired ディレクティブ](inf-inboxversionrequired-directive.md)」を参照してください。 | なし | なし |

 

 **メモ**  **1 (DRIVERCATEGORY)** : INF ファイルでカテゴリが指定されている場合は、カテゴリを指定するために次の値が許可されます (それぞれ 0 ~ 5)。
 
 
| ドライバーカテゴリ          | 値 | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|-------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PrintFax.Printer         | 0     | コンピューターに接続されているプリンター (ローカルまたはネットワークプロトコル経由)、または別のコンピューター上の物理プリンターへのプロキシのいずれかを表す印刷キュー。 ユーザーが物理プリンターに印刷すると、その結果、ドキュメントが印刷された紙になります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| PrintFax.Fax             | 1     | 物理または仮想 fax コンピューターを表す印刷キュー。 ユーザーが fax プリンターに印刷すると、(ユーザーがさらに操作を行った後で) fax が送信されるという結果になります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax. Printer. ファイル    | 2     | ソフトコピードキュメントを生成する印刷キュー。 ユーザーがファイルプリンターに印刷すると、ユーザーはまずファイル名を入力する必要があり、スプーラはそのファイルに出力を送信します。 ファイルプリンターは常にファイル名を必要としますが、他のユーザー入力は必要ありません。 ユーザーがファイル名を指定するオプションがない場合、アプリはスプーラで使用可能なファイル名を生成します。 ファイルプリンターの一般的な例として、Microsoft XPS Document Writer (MXDW) と PDF ライターがあります。                                                                                                                                                                                                                                                 |
| PrintFax. Printer. Virtual | 3     | 印刷スプーラーに対して非透過の印刷データに対して何らかの操作を実行するドライバーを持つ印刷キュー。 ユーザーが仮想プリンターに出力するときに、結果として、印刷されたドキュメントがコンピューター上のどこかに保存されているか、別のアプリケーションに送信されているか、電子メールで送信されている可能性があります。 仮想プリンターへの印刷の一般的な例として、印刷されたドキュメントが Microsoft Office OneNote プリンターに送信されるというシナリオがあります。 ユーザーが仮想プリンターに印刷することを選択した場合、ドライバーまたはその他のドライバーコンポーネントによって開始される、さらにユーザーの操作が必要になることがあります。 詳細については、「[プリンターの INF ファイルの仮想プリンター](virtual-printers-in-printer-inf-files.md)」を参照してください。 |
| PrintFax. Printer. Service | 4     | 印刷サービスを表す印刷キュー。 ユーザーがサービスへの印刷を選択すると、その結果 (ユーザーがさらに操作を行った後)、サードパーティの印刷サービスが印刷されたコンテンツを受け取ることになります。 ユーザーは、物理的な事業所に移動して、印刷出力を取得できます。                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax.Printer.3D      | 5     | 3D プリンターのデータストリームを表す印刷キュー。 このカテゴリが、誤って2D プリンター (通常使うプリンター) に指定されている場合、2D プリンターは単にデータストリームの2D コンテンツを出力します。 3D プリンターに対してこのカテゴリが正しく指定されていても、2D データストリームが3D プリンターに送信された場合、3D プリンターは出力を生成しません。                                                                                                                                                                                                                                                                                                                                                                |

 

また、v4 印刷ドライバーはマニフェストファイルを使用することにも注意してください。 詳細については、「 [V4 ドライバーマニフェスト](v4-driver-manifest.md)」を参照してください。

 

**注**  **2 (ExcludeFromSelect)** : **[デバイスの選択**] ダイアログまたはプリンターの追加ウィザードに表示されないデバイスの*デバイス ID* 。 プリンタの場合、これには、デバイスの説明が重複しているデバイスのすべての PnP エントリが INF ファイルに含まれます。たとえば、赤外線と並列の列挙、または別のバス用の複数のエントリを持つデバイスなどです。 ExcludeFromSelect エントリは、このテーブル内の他のすべてのものとは異なり、INF ファイルのコントロールフラグセクションに表示される必要があります。 詳細については、「 [**INF ControlFlags」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)を参照してください。

 

**メモ**  **3 (VendorSetup)** : VendorSetup エントリが指定されていない場合は、カスタマイズされたセットアップ操作は実行されません。 特に、VendorSetup INF エントリを使用する場合を除き、プリントプロセッサ、印刷モニター、またはプリンタードライバーのインストール中にユーザーインターフェイスを使用することはできません。 このエントリの詳細については、「カスタマイズされた[プリンターセットアップ操作](customized-printer-setup-operations.md)」を参照してください。

 

**重要**  : VendorSetup は現在非推奨とされており、開発した*新しい*v3 または v4 ドライバーでは使用できません。 この VendorSetup に関する情報は、参照専用、または既にこの INF ディレクティブを使用している既存の v3 ドライバーのメンテナンスのために提供されています。

 

プリンターの INF ファイルのエントリは、通常、[プリンターの inf ファイルのデータセクション](printer-inf-file-data-sections.md)内で指定されます。 例については、「[プリンターの INF ファイルのサンプル](sample-printer-inf-files.md)」を参照してください。

### <a href="" id="ddk-languagemonitor-value-format-gg"></a>LanguageMonitor 値の形式

プリンターの INF ファイルに LanguageMonitor エントリが含まれている場合、値の形式は次のようになります。

LanguageMonitor = " *Monitorname* , *MonitorDLLName* "

ここで、 *Monitorname*は、モニターの表示名を表すテキスト文字列です。 *MonitorDLLName*は、モニター DLL のファイル名です。

### <a href="" id="ddk-printprocessor-value-format-gg"></a>PrintProcessor 値の形式

PrintProcessor エントリがプリンターの INF ファイルに含まれている場合、値の形式は次のようになります。

PrintProcessor = " *Printprocessorname* , *PrintProcessorDLLName* "

*Printprocessorname*は、印刷プロセッサの表示名を表すテキスト文字列で、 *PrintProcessorDLLName*は DLL のファイル名です。

### <a href="" id="ddk-dependent-files-gg"></a>依存ファイル

Windows 2000 以降では、依存ファイルはプリンタードライバーファイルであり、プリンターの INF ファイルの[インストールセクション](printer-inf-file-install-sections.md)には[66000 があり](printer-dirids.md)ますが、driverfile、データファイル、ConfigFile、または HelpFile エントリには割り当てられません。

次の例では、3つの依存ファイルをインストールする INF ファイルからの抜粋を示しています。これは、プリンタードライバーのディレクトリ (つまり、dirid 66000 で指定されたディレクトリ) にコピーすることによって行います。

```cpp
[Contoso]
%PRINTER_MODEL_123%=Contoso_Install_Section,LPTENUM\Contoso_1284.4_P29C5
...
[Contoso_Install_Section]
CopyFiles=@Contoso.ini,@Contoso.xml,@Contoso.dll
...
[DestinationDirs]
DefaultDestDir=66000
...
[Strings]
PRINTER_MODEL_123 = "Contoso Printer Model 123"
```

この例では、Contoso .ini はプリンターの INI ファイルであり、contoso .xml は bidi 拡張ファイルであり、Contoso .dll はカスタマイズされたコンポーネントです。 プリンター INI ファイル、bidi 拡張ファイル、およびカスタマイズされたコンポーネントの詳細については、「カスタマイズされた[ドライバーコンポーネント](installing-customized-driver-components.md)と[双方向通信スキーマ](bidirectional-communication-schema.md)のインストール」を参照してください。

[ポイントアンドプリント](introduction-to-point-and-print.md)操作では、ドライバーとドライバーに依存するファイルの両方がクライアントにインストールされます。

各プリンターモデルには、最大64の依存ファイルを指定できます。

## <a name="related-topics"></a>関連トピック
[双方向通信スキーマ](bidirectional-communication-schema.md)  
[**INF ControlFlags セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)  
[カスタマイズされたドライバーコンポーネントのインストール](installing-customized-driver-components.md)  
[ポイントアンドプリント](introduction-to-point-and-print.md)  
[プリンタ INF ファイルインストールセクション](printer-inf-file-install-sections.md)  
[V4 ドライバーマニフェスト](v4-driver-manifest.md)  



