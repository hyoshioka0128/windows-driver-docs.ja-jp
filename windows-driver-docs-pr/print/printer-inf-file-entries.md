---
title: プリンターの INF ファイルのエントリ
description: プリンターの INF ファイルのエントリ
ms.assetid: 897072bb-e481-4c8d-a2bf-57b19c69ac0e
keywords:
- WDK の INF ファイルを印刷するエントリ
- WDK プリンターの依存ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29398cffcde34e28002c3d7e3a4a034afb5dcd8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559702"
---
# <a name="printer-inf-file-entries"></a>プリンターの INF ファイルのエントリ





プリント サーバーにプリンターをインストールするインストール アプリケーションは、呼び出す必要があります、スプーラーの**AddPrinterDriverEx**関数を呼び出して、スプーラーのドライバー ファイルを読み込んで**AddPrinter**関数プリンターをサーバーで使用できるようにします。

**AddPrinterDriverEx**関数には、ドライバーが必要です\_情報\_、入力として 3 つの構造と**AddPrinter**関数に必要なプリンター\_情報\_。入力として 2 つの構造体。 既定の Windows 2000 またはそれ以降のプリンター クラスのインストーラー、Ntprint.dll、関数が呼び出される前に、これらの構造体に配置する必要があります文字列値を取得するプリンターの INF ファイルを読み取ります。


**AddPrinterDriverEx**と**AddPrinter**関数は、ドライバーと\_情報\_3 とプリンターの\_情報\_2 つの構造は、Microsoft Windows SDK のドキュメントで説明します。

Ntprint.dll を認識するプリンター ドライバーの INF ファイルのエントリのセットが定義されています。 これらのエントリには、次の形式があります。

*EntryName* = *Value*

場所*EntryName*エントリを識別する文字列と*値*エントリに割り当てられている文字列値です。

次の表には、プリンターの INF ファイルに含める必要がある INF ファイルのエントリが一覧表示します。 各エントリでは、テーブルには、次が含まれています。

-   この値は、エントリに割り当てる必要があります。

-   Ntprint.dll が、エントリが定義されていない場合に使用する既定値。

-   Ntprint.dll エントリの値へのポインターを格納する構造体のメンバー。

| INF ファイルのエントリ       |Value|(エントリが指定されていない) 場合、既定値|構造体のメンバー |
|----------------------|-----|-------------|-----------------------------------------|
| ConfigFile           | ドライバーの名前[プリンター インターフェイス DLL](printer-interface-dll.md)します。 | DriverFile 指定された値。 | **pConfigFile**ドライバーのメンバー\_情報\_3 つの構造 (Windows SDK のドキュメントで説明) |
| データ ファイル             | PPD ファイルなどのドライバーの関連するデータ ファイルの名前。 | INF ファイル内のドライバーのセクション名。 | **pDataFile**ドライバーのメンバー\_情報\_3 構造 |
| DefaultDataType      | NT-ベースのオペレーティング システムで使用できません。 |||
| DriverCategory       | 参照してください**注 1**、次のテーブル。 | INF ファイルは、(ほとんど v3 ドライバー) などのカテゴリでドライバーを指定しない場合、ドライバーのカテゴリは、ことが前提です**PrintFax.Printer**します。 | なし |
| DriverFile           | ドライバーの名前[プリンター グラフィックス DLL](printer-graphics-dll.md)します。 | INF ファイル内のドライバーのセクション名。 | **pDriverPath**ドライバーのメンバー\_情報\_3 構造 |
| ExcludeFromSelect    | 参照してください**注 2**、次のテーブル。 | なし | なし |
| HelpFile             | インターフェイスの DLL のヘルプ ファイルの名前。 | なし。 ヘルプ ファイルが指定されていません。 | **pHelpFile**ドライバーのメンバー\_情報\_3 構造 |
| LanguageMonitor      | プリンタ ドライバに関連する言語モニターの名前。 参照してください、 **LanguageMonitor 値形式**セクション。 | なし。 言語モニターが指定されていません。 | **pMonitorName**ドライバーのメンバー\_情報\_3 構造 |
| PrintProcessor       | プリンター キューに関連するプリント プロセッサの名前。 参照してください、 **PrintProcessor 値形式**セクション。 | 既定のプリント プロセッサ (WinPrint) が使用されます。 | **pPrintProcessor**ドライバーのメンバー\_情報\_2 の構造 (Windows SDK のドキュメントで説明) |
| VendorSetup          | 処理するベンダーから提供された DLL 内の関数の名前、[プリンター セットアップの操作をカスタマイズ](customized-printer-setup-operations.md)します。 | なし。 参照してください**注 3**、次のテーブル。 | なし |
| InboxVersionRequired | INF を参照するすべてのコア ドライバーの許容される最小バージョン。 InboxVersionRequired の詳細については、[INF InboxVersionRequired ディレクティブ](inf-inboxversionrequired-directive.md)を参照してください。 | なし | なし |

 

 **注**  **1 (DriverCategory)**:これらは、許可されている値、INF ファイルでは、カテゴリを指定する場合 (0 ~ 5 それぞれ) カテゴリを指定します。
 
 
| ドライバー カテゴリ          | Value | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|-------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PrintFax.Printer         | 0     | 印刷キューを表すか、プリンターをコンピューターに接続 (を通じて、ローカルまたはネットワーク プロトコル)、または別のコンピューター上の物理プリンターへのプロキシ。 ユーザーが物理プリンターに印刷、用紙に印刷されたドキュメントになります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| PrintFax.Fax             | 1     | Fax の物理または仮想マシンを表す印刷キューです。 ユーザーが fax プリンターに印刷 (可能性があるユーザーの関与) した後、結果は fax が送信されることが。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax.Printer.File    | 2     | ドキュメントの論理的なコピーを生成する印刷キューです。 ユーザーがファイルのプリンターに印刷し、ユーザーが、ファイル名を入力する必要があります最初、スプーラーは、そのファイルに印刷出力を送信するし。 ファイルのプリンターは常にファイル名が必要ですが、他のユーザー入力は不要します。 ユーザーがファイル名を指定するためのオプションがない場合に、アプリは、スプーラーに使用可能になるファイル名を生成します。 ファイルのプリンターの一般的な例は、Microsoft XPS ドキュメント ライター (MXDW) と PDF のライターです。                                                                                                                                                                                                                                                 |
| PrintFax.Printer.Virtual | 3     | 印刷キューが不透明に印刷スプーラーは印刷データに対して何らかの操作を実行するためのドライバーです。 ユーザーが仮想プリンターに印刷、いくつかの可能な結果には、コンピューターが別のアプリケーションに送信される、または電子メールで送信されるどこかに保存されている印刷したドキュメントが含まれます。 仮想プリンターで印刷の一般的な例は、Microsoft Office OneNote のプリンターに印刷されるドキュメントの送信先のシナリオです。 ユーザーが仮想プリンターに印刷すると、ときに、ドライバーまたはその他のいくつかのドライバー コンポーネントによって開始された、それ以上のユーザーの対話の必要性があります。 詳細については、[プリンター INF ファイルでの仮想プリンター](virtual-printers-in-printer-inf-files.md)を参照してください。 |
| PrintFax.Printer.Service | 4     | 印刷サービスを表す印刷キューです。 サービスに印刷するユーザーを選択するときに、結果 (可能性があるユーザーの関与) した後は、サードパーティの印刷サービスが、印刷コンテンツを受信できます。 ユーザーはことができますし、印刷出力を取得するビジネスの物理的な場所に移動します。                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax.Printer.3D      | 5     | 3D プリンターのデータ ストリームを表す印刷キューです。 2D プリンター (通常プリンター) のこのカテゴリを誤って指定すると場合、2D のプリンターは単にデータ ストリームの 2D のコンテンツを出力します。 このカテゴリは、3 D プリンターを正しく指定されて、2 D のデータ ストリームが 3D のプリンターに送信される場合、3 D プリンターでは、この出力は生成されません。                                                                                                                                                                                                                                                                                                                                                                |

 

V4 印刷ドライバーがマニフェスト ファイルを使用することにも注意してください。 詳細については、[V4 ドライバー マニフェスト](v4-driver-manifest.md)を参照してください。

 

**注**  **2 (ExcludeFromSelect)**:*デバイス ID*で表示しないデバイスの**デバイスの**ダイアログまたは プリンターの追加ウィザード。 このプリンターを INF ファイルで重複するデバイスの説明を持つデバイスのすべての PnP エントリが含まれていますたとえば、赤外線および並列列挙のため、または別のバスの複数のエントリがあるデバイスです。 この表で、他のすべてとは異なり、ExcludeFromSelect エントリは、INF ファイルの制御フラグ セクションに表示する必要があります。 参照してください[ **INF ControlFlags セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546342)詳細についてはします。

 

**注**  **3 (VendorSetup)**:VendorSetup エントリが指定されていない場合は、カスタマイズされたセットアップ操作は実行されません。 具体的には、ユーザー インターフェイスは許可されていませんプリント プロセッサ、印刷のモニター、またはプリンター ドライバーのインストール中を除く VendorSetup INF エントリを使用しています。 このエントリの詳細については、[プリンター セットアップの操作のカスタマイズ](customized-printer-setup-operations.md)を参照してください。

 

**重要な**  :VendorSetup が現在は非推奨し、で使用する必要がありますいない*新しい*v3 または v4 ドライバーを開発します。 既にこの INF ディレクティブを使用している既存の v3 ドライバーのメンテナンスのみ、または、参照のこの VendorSetup に関する情報が提供されます。

 

プリンター INF ファイルのエントリが内で指定された通常[プリンター INF ファイルのデータ セクション](printer-inf-file-data-sections.md)します。 例については、、[サンプル プリンター INF ファイル](sample-printer-inf-files.md)を参照してください。

### <a href="" id="ddk-languagemonitor-value-format-gg"></a>LanguageMonitor 値の形式

LanguageMonitor エントリは、プリンターの INF ファイルに含めるとき、値の形式のとおりです。

LanguageMonitor=" *MonitorName* , *MonitorDLLName* "

場所*モニター*モニターの表示名を表すテキスト文字列と*MonitorDLLName*モニター DLL のファイルの名前です。

### <a href="" id="ddk-printprocessor-value-format-gg"></a>PrintProcessor 値の形式

PrintProcessor エントリは、プリンターの INF ファイルに含めるとき、値の形式のとおりです。

PrintProcessor=" *PrintProcessorName* , *PrintProcessorDLLName* "

場所*PrintProcessorName*プリント プロセッサの表示名を表すテキスト文字列と*PrintProcessorDLLName* DLL のファイルの名前です。

### <a href="" id="ddk-dependent-files-gg"></a>依存ファイル

依存ファイルに含まれているプリンタ ドライバ ファイルは、Windows 2000 以降で、[プリンター INF ファイル インストール セクション](printer-inf-file-install-sections.md)で、 [dirid](printer-dirids.md) 66000 が DriverFile、DataFile、ConfigFile に割り当てられていません、またはヘルプ ファイルのエントリ。

次の例では、(指定されている、ディレクトリに dirid 66000 によって)、プリンター ドライバー ディレクトリにコピーして、次の 3 つの依存ファイルをインストールする INF ファイルからの抜粋を示します。

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

この例で Contoso.ini はプリンターの INI ファイル、Contoso.xml は双方向の拡張ファイル、および Contoso.dll はカスタマイズされたコンポーネント。 プリンターの INI ファイル、双方向の拡張ファイル、およびカスタマイズされたコンポーネントに関する詳細については、[カスタマイズされたドライバー コンポーネントをインストール](installing-customized-driver-components.md)と[双方向通信スキーマ](bidirectional-communication-schema.md)を参照してください。

[ポイント アンド プリント](introduction-to-point-and-print.md)操作は、ドライバーと、クライアント ドライバーに依存するファイルの両方をインストールします。

プリンター モデルごとに最大で 64 の依存ファイルを指定できます。

## <a name="related-topics"></a>関連トピック
[双方向通信のスキーマ](bidirectional-communication-schema.md)  
[**INF ControlFlags セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546342)  
[カスタマイズされたドライバー コンポーネントをインストールします。](installing-customized-driver-components.md)  
[ポイント アンド プリント](introduction-to-point-and-print.md)  
[プリンター INF ファイルのインストールのセクション](printer-inf-file-install-sections.md)  
[V4 ドライバー マニフェスト](v4-driver-manifest.md)  



