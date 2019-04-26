---
title: Inf2Cat を使ったカタログ ファイルの作成
description: Inf2Cat を使ったカタログ ファイルの作成
ms.assetid: 93dea980-eb66-40f0-ac6b-0adaf8376154
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea029f19a656ba32313198b889eba0d1b3c7f03d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339407"
---
# <a name="using-inf2cat-to-create-a-catalog-file"></a>Inf2Cat を使ったカタログ ファイルの作成


Inf2Cat ツールは、いずれかのカタログ ファイルを作成するために使用できます[ドライバー パッケージ](driver-packages.md)INF ファイルを持ちます。 Inf2Cat とコマンドライン引数の詳細については、次を参照してください。 [ **Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089)します。

**注**  する前に、Windows Server 2008 Windows Driver Kit (WDK)、Inf2Cat ツールは、WDK ツールの一部であったされません。 ただし、このツールは Winqual Submission ツールと共にインストールされます。 Winqual Submission ツールをダウンロードするには Microsoft [Inf2Cat FAQ](https://go.microsoft.com/fwlink/p/?linkid=79443) web サイト。 Winqual Submission ツール パッケージがインストールされると、 [ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089) Program Files (x86) に配置されます\\システム ドライブ上の Microsoft Winqual Submission Tool フォルダー。

 

このトピックでは、作成する方法を説明します、[カタログ ファイル](catalog-files.md)ドライバー パッケージの INF ファイルから。 この例では、INF ファイルでは、 *ToastPkg*サンプル ドライバー パッケージが使用されます。 この INF ファイルの名前は、WDK のインストール ディレクトリ内で*toastpkg.inf*にある、 *src\\全般\\トースター\\toastpkg\\inf*ディレクトリ。

カタログの名前のファイルを[ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)が生成されますが、CatalogFile ディレクティブによって指定されます。 1 つ以上のこれらのディレクティブが内で宣言された、 [ **INF バージョン セクション**](inf-version-section.md)の INF ファイル。 INF**バージョン**のセクション、 *toastpkg.inf*ファイルを次に示します。

```cpp
[Version]
Signature="$WINDOWS NT$"
Class=TOASTER
ClassGuid={B85B7C50-6A01-11d2-B841-00C04FAD5171}
Provider=%ToastRUs%
DriverVer=09/21/2006,6.0.5736.1
CatalogFile.NTx86  = tostx86.cat
CatalogFile.NTIA64 = tostia64.cat
CatalogFile.NTAMD64 = tstamd64.cat
```

この 2 つのことに注意してください[ **INF バージョン セクション**](inf-version-section.md):

1. [ **INF バージョン セクション**](inf-version-section.md)ドライバー パッケージをサポートする Windows バージョンごとに 1 つずつ、3 つの別のカタログ ファイルを宣言します。 ときに[ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)がで指定された各 Windows バージョンのカタログ ファイルを作成、実行、 **/os**オプション。

   たとえば、Inf2Cat はカタログ ファイルを作成します。 *toastamd64.cat*コマンドライン引数/os:Vista_X64 を使用する場合。 同様に、ツールは、カタログ ファイルを作成します。 *toastx86.cat*場合、 **/os:**<em>Vista_X86</em>オプションを使用します。

2. [ **DriverVer ディレクティブ**](inf-driverver-directive.md)古いタイムスタンプおよびバージョンを INF のバージョンのセクションを宣言します。

   使用する前に[ **Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089)、する必要があること確認する INF ファイルの**DriverVer**ディレクティブが現在の時刻スタンプとバージョンの値。 これは必要、[ドライバー パッケージ](driver-packages.md)をインストールして、テスト コンピューター上のパッケージの以前にインストールされたバージョンが置き換えられます。

   使用することができます、 [Stampinf](https://msdn.microsoft.com/library/windows/hardware/ff552786)で時刻のスタンプとバージョンの値を更新するためのツール、 **DriverVer**ディレクティブ。 たとえば、更新するため、 **DriverVer**ディレクティブで、 *toastpkg.inf*、次のコマンドを実行して<em>:</em>

   ```cpp
   stampinf -f toastpkg.inf -d 09/01/2008 -v 9.0.9999.0
   ```

次のコマンドラインを使用して、Inf2Cat ツールを使用するカタログ ファイルを作成する方法を示しています、 *Toastpkg.inf*ファイル。

```cpp
Inf2cat.exe /driver:src\general\toaster\toastpkg\toastcd\ /os:Vista_x64
```

各項目の意味は次のとおりです。

- **/Driver**オプションは、1 つまたは複数の INF ファイルを含むディレクトリを指定します。 このディレクトリ内でそれらの INF ファイルを 1 つまたは複数の CatalogFile ディレクティブを含むカタログ ファイルが作成されます。 CatalogFile ディレクティブの詳細については、次を参照してください。 [ **INF バージョン セクション**](inf-version-section.md)します。

  のみ、この例では、 *toastpkg*.inf INF ファイルが指定した内にある*src\\全般\\トースター\\toastpkg\\toastcd*ディレクトリ。

- **/Os:**<em>Vista_x64</em>オプションは、カタログ ファイルは、Windows Vista の 64 ビット バージョンを指定します。 Inf2Cat ツールには、要求した Windows バージョンにカタログ ファイルの名前は一致します。 以降、 *toastpkg*.inf INF ファイルには NTAMD64 プラットフォーム拡張機能を持つ CatalogFile ディレクティブが含まれています、Inf2Cat という名前のカタログ ファイルが作成されます*tstamd64.cat します。*

  1 つまたは複数の Windows バージョンを指定することがあります、 **/os:** オプション。 たとえば場合、 **/os:**<em>Vista_x64、Vistax32</em>指定すると、Inf2Cat を作成、 *tstamd64.cat*と*tstx86.cat*ためにファイルINF CatalogFile ディレクティブの*toastpkg*.inf INF ファイル。

ツールのコマンドライン引数の詳細については、次を参照してください。 [ **Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089)します。

 

 





