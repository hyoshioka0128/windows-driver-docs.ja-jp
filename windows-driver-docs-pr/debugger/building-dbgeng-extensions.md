---
title: DbgEng 拡張機能の構築
description: DbgEng 拡張機能の構築
ms.assetid: e2cf8a01-2099-4ad7-98ac-1a20c76a2e0a
keywords:
- DbgEng 拡張機能の構築
- ビルド ユーティリティ (build.exe) DbgEng 拡張機能の作成
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 419d84f2da870f090f236b60ffd72dcad34d56fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570910"
---
# <a name="building-dbgeng-extensions"></a>DbgEng 拡張機能の構築


## <span id="ddk_building_dbgeng_extensions_dbx"></span><span id="DDK_BUILDING_DBGENG_EXTENSIONS_DBX"></span>


すべてのデバッガー拡張機能はコンパイルされ、Visual Studio を使用して構築する必要があります。 ビルド ユーティリティはデバッガーの拡張機能では使用されません。

Visual Studio でプロジェクトをビルドに関するドキュメントについてを参照してください[Visual Studio での C++ プロジェクトをビルドします。](https://msdn.microsoft.com/library/7s88b19e.aspx)

拡張機能をビルドするには、次の手順を使用します。

**デバッガーの拡張機能を構築するには**

1.  開く、 **dbgsdk.sln** Visual Studio でサンプル プロジェクト。

2.  Include および lib ファイル プロジェクトの設定を確認します。 場合 *% デバッガー*ルートを表す、Windows のツールをデバッグ インストールの設定する次のようにします。

    ```text
    Include Path 
    %debuggers%\sdk\inc
    Library Path
    %debuggers%\sdk\lib
    ```

    別の場所にこれらのヘッダーとライブラリを移動した場合は、その場所を指定します。

3.  選択**ビルド**し**ソリューションのビルド**Visual Studio のメニューから。

 

 





