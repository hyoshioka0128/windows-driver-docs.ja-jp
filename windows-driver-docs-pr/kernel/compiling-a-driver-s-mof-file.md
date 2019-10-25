---
title: ドライバーの MOF ファイルのコンパイル
description: ドライバーの MOF ファイルのコンパイル
ms.assetid: 0a4ab163-3e2c-48e9-9659-756d35ad445f
keywords:
- WMI WDK カーネル、発行スキーマ
- WMI スキーマの発行 WDK
- スキーマ発行 WDK WMI
- MOF ファイル WDK WMI
- MOF ファイルのコンパイル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1692dcd7b8639161c03ecd02a2a88f8a4940fd0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837073"
---
# <a name="compiling-a-drivers-mof-file"></a>ドライバーの MOF ファイルのコンパイル





WMI データとイベントブロックを定義する MOF ファイルをコンパイルするには、Microsoft Windows オペレーティングシステムに含まれている、Mofcomp.exe という MOF コンパイラを使用します。 使用する構文は以下のとおりです。

```cpp
 mofcomp -WMI -B:filename.bmf filename.mof
```

上記の構文では、次の項目が表示されます。

<a href="" id="-wmi"></a> **-WMI**  
WMI で使用するために、*ファイル名 .mof*内のすべてのクラスを検証します。 クラス定義が無効な場合、Mofcomp.exe は出力ファイル*filename. bmf*を削除します。 **-WMI**が省略されている場合は、 [Wmimofck](using-wmimofck-exe.md)を実行してクラスを検証する必要があり*ます。* ドライバーは、WMI スイッチを使用するか、Wmimofck を実行して MOF を検証する必要があります。 そうしないと、MOF ファイルが WMI スキーマに正しく読み込まれないことがあります。

<a href="" id="-b-filename-bmf"></a> **-B:** <em>ファイル名。 bmf</em>  
コンパイラが、CIMOM オブジェクトリポジトリを変更することなく、プラットフォームに依存しないバイナリバージョンの MOF ファイルを*ファイル名. bmf*に作成するように要求します。

<a href="" id="filename-mof"></a>*ファイル名 .mof*  
入力 MOF ファイルの名前を指定します。

Mofcomp.exe の使用方法の詳細については、コマンドプロンプトウィンドウを開き、「 **mofcomp.exe/?** 」と入力してください。

Mofcomp.exe の詳細については、「」の「 [mofcomp.exe](https://go.microsoft.com/fwlink/p/?linkid=51316) 」および「Windows SDK」を参照してください。

コンパイルされた MOF ファイルをリソースとしてドライバーのバイナリイメージに含めるには、ドライバーのリソーススクリプト (RC) ファイルに次の行を追加します。

**MOFRESOURCE MOFDATA** *. bmf*

ドライバーは、登録要求に応答してその MOF リソース名を指定します ( [**irp\_\_reginfo**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)または[**Irp\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)データパスに設定さ**れたパラメーター**を使用した要求\_EX 要求)。

-   ドライバーが wmi の Irp を処理するために WMI ライブラリルーチンを使用している場合は[ *、そのドライバー*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)のリソース名を指定します。

-   ドライバーが WMI Irp を直接処理している場合は、ドライバーが WMI に渡す、 [**wmi のリソース**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)名を指定します。

REGINFO と**irp\_\_** \_reginfo\_EX の要求に対する**irp\_** 処理の詳細については、「 [WMI Data Provider としての登録](registering-as-a-wmi-data-provider.md)」を参照してください。

Wmi iibrary ルーチンを使用して WMI Irp を処理する方法の詳細については、「 [Wmi 要求の処理](handling-wmi-requests.md)」を参照してください。

実行可能ファイルにリソースを定義して含める方法の詳細については、「Microsoft Windows SDK」を参照してください。

 

 




