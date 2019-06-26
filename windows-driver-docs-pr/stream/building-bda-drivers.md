---
title: BDA ドライバーの構築
description: BDA ドライバーの構築
ms.assetid: 2272fa18-5102-443e-8728-f256444ab044
keywords:
- ドライバーのアーキテクチャの WDK AVStream、ドライバーの構築のブロードキャストします。
- BDA WDK AVStream、ドライバーの構築
- ドライバー WDK、BDA 構築
- ユーティリティ、WDK BDA をビルドします。
- WDK BDA マクロ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb7dca13d40a74f03c75b4056a959a06070f1be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386675"
---
# <a name="building-bda-drivers"></a>BDA ドライバーの構築





**注**  以降 Windows 8 では、WDK ビルド環境は使用しなくなりました Build.exe します。 参照してください[WDK と Visual Studio ビルド環境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)します。 次の説明には、Windows 7 の WDK バージョンを使用して、ドライバーをビルドする場合にのみが適用されます。 以前のバージョン。

 

Microsoft Windows Driver Kit (WDK) を使用するには、ブロードキャスト ドライバーのアーキテクチャ (BDA) ドライバーをビルドします。 BDA ドライバーをビルドする WDK ビルド環境ウィンドウを開き、WDK のメイン ソース ディレクトリの適切な BDA ドライバーのソース コードのサブディレクトリに変更し、使用、**ビルド**コマンド。 **ビルド**コマンドから BDA ドライバーを構築する方法の手順の取得、*ソース*BDA ドライバーのソース コードのサブディレクトリに存在するファイル。

ビルド ユーティリティ、WDK のビルド環境、マクロと環境変数をビルド ユーティリティを制御および BDA ドライバーのビルドに必要なファイルの詳細についてを参照してください「を使用して、ビルド ユーティリティ」および「ビルド ユーティリティ リファレンス」Windows 7 の WDK ドキュメント (build 7600) です。

次の一覧が、BDA で使用するマクロ名を含む*ソース*ファイルを開き、BDA ドライバーの構築に使用する方法について説明します。

<a href="" id="--------targetname-------"></a> TARGETNAME   
WDK は、ドライバーを作成するときにこの名前を持つビルドできるように、BDA ドライバーの名前に設定します。 次のコード例に示します。

```make
TARGETNAME=BDAsampl  # WDK builds the driver as BDAsampl.sys
```

<a href="" id="--------targetpath-------"></a> TARGETPATH   
組み込みのドライバーのインストール先ディレクトリを設定します。 注によってかどうか、ビルド環境は、「無料」または「オン」は、ビルドを使用できる\_ALT\_DIR 変数に"fre"または"chk"を追加する、 \\obj サブディレクトリ ビルド コマンドがディレクトリの下に作成します。含む、*ソース*ファイル。 次のコード例に示します。

```make
TARGETPATH=obj$(BUILD_ALT_DIR) # built driver in \objfre or \objchk
```

<a href="" id="--------targettype-------"></a> TARGETTYPE   
次のコードに示すように、ドライバー (ではなく、プログラムまたは DLL ではなど) としてビルドするファイルの種類を設定します。

```make
TARGETTYPE=DRIVER  # WDK builds the driver as *.sys
```

<a href="" id="--------targetlibs-------"></a> TARGETLIBS   
BDA ドライバーのサンプルのソースをリンクする必要があります、ライブラリ ファイルをポイントします。 BDA ドライバーは、次のコード例に示すようにライブラリにリンクする必要がありますには少なくとも。

```make
TARGETLIBS=..\..\..\..\lib\ks.lib \
           ..\..\..\..\lib\ksguid.lib \
           ..\..\..\..\lib\BdaSup.lib
```

<a href="" id="--------includes---"></a> 含まれています   
BDA ドライバーのサンプルのソースをコンパイルするために必要とするヘッダー ファイルを検索するパスの一覧をポイントします。 次のコード例に示します。

```make
INCLUDES=..\..\..\..\inc; \
    $(DDK_INC_PATH)\wdm; 
```

<a href="" id="--------sources-------"></a> ソース   
ドライバーのビルドをコンパイルする必要があるソース ファイルの一覧をポイントします。 ファイルがディレクトリ内に存在する必要があります、*ソース*ファイルが存在します。 次のコード例に示します。

```make
SOURCES= \
    ObjDesc.cpp     \
    inpin.cpp     \
    outpin.cpp    \
    Filter.cpp      \
    Device.cpp      \
    bdaguid.c       \
    BDAsampl.rc
```

<a href="" id="--------drivertype-------"></a> DRIVERTYPE   
WDM 次のコードに示すようにするには、ドライバーの種類を設定します。

```make
DRIVERTYPE=WDM
```

<a href="" id="--------use-mapsym-------"></a> 使用\_MAPSYM   
生成 *.sym*に加えてシンボル ファイルを *.pdb*シンボル ファイル。 これらのファイル名のアドレスにマップします。 Windows 98 でのデバッグに必要なは、このマクロを設定/Me プラットフォーム。 このマクロは、次の例に示すように設定します。

```make
USE_MAPSYM=1
```
