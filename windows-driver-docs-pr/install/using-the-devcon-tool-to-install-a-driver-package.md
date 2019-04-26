---
title: ドライバー パッケージをインストールするための DevCon ツールの使用
description: ドライバー パッケージをインストールするための DevCon ツールの使用
ms.assetid: d77573e0-7866-46a5-88bc-c911bbd2a165
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e58b8cf9c61d1b21ae60adf366e07cfa741cb0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339385"
---
# <a name="using-the-devcon-tool-to-install-a-driver-package"></a>ドライバー パッケージをインストールするための DevCon ツールの使用


このトピックの例では、 *ToastPkg*サンプル[ドライバー パッケージ](driver-packages.md)します。 WDK のインストール ディレクトリ内で、パッケージのソース ファイル内にある、 *src\\全般\\トースター\\toastpkg\\toastcd*ディレクトリ。 構築して、デジタル署名されたドライバー パッケージのこの後は、ドライバー パッケージをディレクトリにコピー *c:\\トースター*テスト コンピューター。

DevCon を使用して、ドライバー パッケージをインストールするには、次の操作を行います。

1.  DevCon ツールを使用するには、ユーザーは、テスト コンピューターの Administrators グループのメンバーであるし、DevCon を管理者特権でコマンド プロンプトから実行する必要があります。 管理者特権のコマンド プロンプト ウィンドウを開くには、デスクトップ ショートカットを作成*Cmd.exe*を右クリックし、 *Cmd.exe*ショートカット、および選択**管理者として実行**します。

2.  管理者特権でコマンド プロンプト ウィンドウで、次のように入力します。

    ```cpp
    devcon.exe install c:\toaster\toastpkg.inf {b85b7c50-6a01-11d2-b841-00c04fad5171}\mstoaster
    ```

    このコマンドラインに、ドライバー パッケージの INF ファイルの場所を指定します (*c:\\トースター\\toastpkg.inf*) と、INF ファイルに指定されているトースター デバイスのハードウェア識別子 (ID)。

 

 





