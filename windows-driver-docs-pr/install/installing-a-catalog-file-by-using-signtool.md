---
title: SignTool を使用したカタログ ファイルのインストール
description: SignTool を使用したカタログ ファイルのインストール
ms.assetid: b3d151af-d49b-468f-a34a-04e5ab875a07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d44c4c1437798c9324cd785b364f83b2aab8999
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366432"
---
# <a name="installing-a-catalog-file-by-using-signtool"></a>SignTool を使用したカタログ ファイルのインストール


[**SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)再頒布可能パッケージのツールではありませんし、再配布インストール アプリケーションを付属したがってすることはできません。 ただし、ツールのマイクロソフト ソフトウェア ライセンス条項に準拠しているように既にインストールされている SignTool をあるコンピューター上で SignTool を使用できます。 A[カタログ ファイル](catalog-files.md)手動でコマンドラインからインストールまたは SignTool の次のコマンドを使用して、コマンドのスクリプトによってインストールされていることができます。

```cpp
SignTool catdb /v /u CatalogFileName.cat
```

各項目の意味は次のとおりです。

-   **Catdb**コマンドが追加またはカタログ ファイルをカタログ データベースから削除する SignTool を構成します。 既定では、SignTool は、システム コンポーネントおよびドライバー データベースに、カタログ ファイルを追加します。

-   **/V**オプションの詳細モードで動作する SignTool を構成します。

-   **/U**オプションの構成と同じ名前を持つ既存のカタログ ファイルを置き換えられないように、必要に応じて、追加するには、カタログ ファイルの一意の名前を生成する SignTool *CatalogFileName.cat*.

-   *CatalogFileName.cat*カタログ ファイルの名前を指定します。

 

 





