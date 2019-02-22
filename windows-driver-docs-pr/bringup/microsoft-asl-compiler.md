---
title: Microsoft ASL コンパイラ
description: Microsoft ASL コンパイラのバージョン 5.0 では、ACPI 5.0 仕様の機能をサポートします。
ms.assetid: E6EC168F-DB4B-461A-874A-F5278E8F9200
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 307ced356e9347b38cd320038465ba5ebff79e6c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560734"
---
# <a name="microsoft-asl-compiler"></a>Microsoft ASL コンパイラ


Microsoft ACPI のソース言語 (ASL) コンパイラ サポートでは、Advanced Configuration and Power Interface Specification、バージョン 5.0 の機能のバージョン 5.0 ([ACPI 5.0 仕様](https://www.uefi.org/specifications))。 ASL コンパイラは、Windows Driver Kit (WDK) で配布されます。 ツールの実行可能ファイルを Asl.exe\\arm\\ACPIVerify、ツール\\arm64\\ACPIVerify、ツール\\x86\\ACPIVerify、またはツール\\x64\\インストールされている、WDK の ACPIVerify ディレクトリ。

## <a name="command-line-options"></a>コマンド ライン オプション


Microsoft ASL コンパイラでは、いくつかのコマンド ライン オプションをサポートします。 使用できるコマンド ライン オプションを一覧表示するコマンドを実行"`asl /?`"コマンド プロンプト ウィンドウでします。

### <a name="usage"></a>使用方法

ASL コンパイラには、次のコマンド ライン オプションがサポートされています。

```console
asl /?
asl [/nologo] /d <BinFile>
asl [/nologo] /u [/Fa=<ASMFile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>] <AMLFile>
asl [/nologo] /tab=<TabSig> [/c] [/Fa=<ASMfile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>]
asl [/nologo] [/Fo=<AMLFile>] [/Fa=<ASMFile>] [/Fl=<LSTFile>] [/Fn=<NSDFile>] <ASLFile>
```

| 構成方法             | 説明                                                                   |
|--------------------|-------------------------------------------------------------------------------|
| ?                  | このヘルプ メッセージを印刷します。                                                      |
| nologo             | ロゴ バナーを抑制します。                                                     |
| Fo =&lt;AMLFile&gt; | DefinitionBlock AML ファイル名をオーバーライドします。                            |
| Fa =&lt;ASMFile&gt; | 生成します。名前のファイルを ASM &lt;ASMFile&gt;します。                           |
| Fn =&lt;NSDFile&gt; | 名前を持つ名前空間のダンプ ファイルを生成&lt;NSDFile&gt;します。                 |
| d                  | テキスト形式でバイナリ ファイルをダンプします。                                            |
| U                  | AML ファイルを逆アセンブルします。ASL ファイル (既定値) またはします。LST ファイルです。               |
| タブ =&lt;TabSig&gt; | ASL テーブルを逆アセンブルします。ASL ファイル (既定値) またはします。LST ファイルです。 非 ASL テーブルをダンプします。TXT ファイルです。 場合&lt;TabSig&gt;は '\*'、すべてのテーブルが ACPI にダンプされます。TXT です。 &lt;TabSig&gt;テーブルの物理アドレスにすることもできます。 |
| c                  | テーブルからバイナリ ファイルを作成します。                                              |

 
## <a name="using-the-microsoft-asl-compilers-acpi-table-load-feature"></a>Microsoft ASL コンパイラの ACPI-テーブル-読み込み機能を使用します。

システムの開発時に、ACPI BIOS のさまざまな構造をシミュレートし、開発システムでテストしたりする方法があると便利です。 Windows オペレーティング システムでは、PC の BIOS ROM からの代わりに、Windows レジストリから読み込まれる特定の ACPI テーブル この機能の使用は、管理者特権が必要し、も、システムでテスト署名を有効にする必要があります。 UEFI セキュア ブートをサポートするシステムでは、テスト署名は有効にすることはできません、および UEFI セキュア ブートが無効になっているか、Windows デバッグ ポリシーがシステムにインストールされている場合を除き、コンパイラのテーブルの読み込み機能は使用できません。

テーブルの読み込み機能を使用するには、オーバー ロードを ACPI テーブルは、次の要件を満たす必要があります。

-   システムの BIOS ROM にある存在しないオーバー ロードするテーブル たとえば、します。 はオーバー ロードできます。ただし、コンピューターは、SSDT を持たない場合は、このレジストリの上書きのメカニズムから読み込まれる、SSDT を強制はできません。
-   テーブルには、Windows の ACPI インタープリター (Acpi.sys ドライバー) によって使用される通常 AML コードを含める必要があります。
-   最新のバージョン番号を持つテーブルが読み込まれます。 テスト用にレジストリに読み込まれるテーブルでは、BIOS ROM にある、同じテーブルより新しいバージョン番号が必要
-   読み込まれるテーブルでは、コンパイル済みの (AML) 形式である必要があり、指定された適切なパラメーターと共に、適切な場所にレジストリに読み込まれます。 ここで説明されているメカニズムは、テーブルを読み込むと、レジストリの構成のすべての側面を処理するために設計されています。

> [!WARNING]
> このトピックで説明されているプロセスは、起動不可能な状態で、Windows システムをしまう可能性があります。 ここで説明した手順を試行する前に、同じマシンに NTFS ファイル システムのサポート (つまり、「セーフ ビルド」) を別のオペレーティング システムへのアクセスがあることを確認します。 このプロセスは、システムの開発者およびテスト担当者のみは提供されており、開発や運用環境の目的で重要なすべてのコンピューターでは使用されませんする必要があります。


### <a name="usage"></a>使用方法

テスト目的で、レジストリ、ACPI テーブルを読み込む、ASL コンパイラは、次のように呼び出されます。

```console
asl.exe /loadtable [-v] [-d] <AMLFile>
```

AMLFile は、レジストリにロードするテーブルを含むコンパイル済みの AML ファイルの名前です。

| 構成方法  | 説明                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| -v      | 詳細モード。 ユーティリティから追加のデバッグ出力をオンにします。                                          |
| -d      | [削除] を選びます。 レジストリから以前に読み込まれた AML ファイルを削除し、すべての関連するレジストリ キーを削除します。|


## <a name="additional-resources"></a>その他の資料

-   [ACPICA ドキュメント](https://acpica.org/documentation/)
-   [ACPI の web サイト](https://www.uefi.org/specifications/)
-   [ACPI のデバッグ](https://msdn.microsoft.com/library/windows/hardware/ff537808)
-   [Acpi.sys:Windows の ACPI ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540493)
-   [電源管理と ACPI](https://msdn.microsoft.com/library/windows/hardware/dn614610)

