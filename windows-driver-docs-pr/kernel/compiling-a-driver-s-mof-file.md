---
title: ドライバーの MOF ファイルのコンパイル
description: ドライバーの MOF ファイルのコンパイル
ms.assetid: 0a4ab163-3e2c-48e9-9659-756d35ad445f
keywords:
- WMI の WDK カーネルでは、スキーマの公開
- 発行の WMI スキーマ WDK
- 発行 WDK WMI スキーマ
- MOF ファイルの WDK WMI
- MOF ファイルのコンパイル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03d163be6616e0d03ab665dafce2faa3b5184f3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383331"
---
# <a name="compiling-a-drivers-mof-file"></a>ドライバーの MOF ファイルのコンパイル





WMI データとイベント ブロックを定義する MOF ファイルをコンパイル、Mofcomp であると呼ばれる MOF コンパイラを使用してオペレーティング システムを Microsoft Windows に付属します。 使用する構文は以下のとおりです。

```cpp
 mofcomp -WMI -B:filename.bmf filename.mof
```

上記の構文で、次のものが表示されます。

<a href="" id="-wmi"></a> **-WMI**  
すべてのクラスを検証します*filename.mof* WMI を使用します。 Mofcomp が出力ファイルを削除する任意のクラス定義が有効でない場合*filename.bmf*します。 場合 **- WMI**が実行を省略すると、 [Wmimofck](using-wmimofck-exe.md)で*filename.bmf*クラスを検証します。 ドライバーはする必要があります WMI スイッチを使用してか、MOF を検証する Wmimofck を実行します。 そのために発生する可能性が MOF ファイルが、WMI スキーマに正しく読み込まれていません。

<a href="" id="-b-filename-bmf"></a> **-B:** <em>filename.bmf</em>  
コンパイラが MOF ファイルのプラットフォームに依存しないバイナリ バージョンを作成することを要求*filename.bmf* CIMOM オブジェクト リポジトリに変更を加えずにします。

<a href="" id="filename-mof"></a>*filename.mof*  
入力の MOF ファイルの名前を指定します。

Mofcomp を使用する方法についての詳細についてに、コマンド プロンプト ウィンドウを開き**mofcomp/でしょうか。** します。

Mofcomp の詳細については、次を参照してください。 [MofComp](https://go.microsoft.com/fwlink/p/?linkid=51316)と Windows SDK の他のトピックです。

ドライバーのバイナリ イメージのリソースとしてコンパイル済みの MOF ファイルを含めるドライバーのリソース スクリプト (RC) のファイルに次の行を追加します。

**MofResource MOFDATA** *filename.bmf*

ドライバーは、登録要求に応答の MOF リソース名を指定します (、 [ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)要求**Parameters.WMI.DataPath** WMIREGISTER に設定)。

-   ドライバーは Irp の WMI を処理するために WMI のライブラリ ルーチンを使用している場合、MOF リソースの名前を指定します。 その[ *DpWmiQueryReginfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)ルーチン。

-   場合は、ドライバーは Irp の WMI を直接処理は、MOF リソースの名前を指定します、 [ **WMIREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)ドライバーが WMI に渡される構造体。

処理の詳細については**IRP\_MN\_REGINFO**と**IRP\_MN\_REGINFO\_EX**要求、確認[WMI データ プロバイダーとして登録する](registering-as-a-wmi-data-provider.md)します。

WMI iibrary ルーチンを使用して WMI Irp の処理の詳細については、次を参照してください。 [WMI 要求の処理](handling-wmi-requests.md)します。

定義して、実行可能ファイルにリソースを含める方法の詳細については、Microsoft Windows SDK を参照してください。

 

 




