---
title: INF ファイルを開くおよび閉じる
description: INF ファイルを開くおよび閉じる
ms.assetid: da270688-4b8b-43b3-afdb-8f31d15ef50c
keywords:
- INF ファイルを開いて、WDK デバイスのインストール
- INF ファイルを閉じる、WDK デバイスのインストール
- INF ファイルを開く
- INF ファイルを閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7234e51fdcf5def3aa4557fd0ced3861be2c8232
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574220"
---
# <a name="opening-and-closing-an-inf-file"></a>INF ファイルを開くおよび閉じる





前に、*デバイス インストール アプリケーション*INF ファイルの情報にアクセスできる、呼び出すことによって、ファイルを開く必要があります、 [ **SetupOpenInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377409)します。 この関数は、INF ファイルを識別するハンドルを返します。

開き、使用する必要がある INF ファイルの名前がわからない場合[ **SetupGetInfFileList** ](https://msdn.microsoft.com/library/windows/desktop/aa377381)ディレクトリ内のすべての INF ファイルの一覧を取得します。

使用する開いているファイルを追加の INF ファイルを追加できますアプリケーションは、INF ファイルを開くと[ **SetupOpenAppendInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377407)します。 ときに後続[SetupAPI](setupapi.md)関数参照 INF ファイルを開く、追加のファイルに格納されているすべての情報にアクセスできます。

呼び出すときに INF ファイルを指定しない場合[ **SetupOpenAppendInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377407)、この関数によって指定されたファイルの追加、 **LayoutFile**内のエントリ、 [ **バージョンの INF セクション**](inf-version-section.md) INF ファイルの呼び出し中に開かれた[ **SetupOpenInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377409)します。

INF ファイルの情報が不要になったときに、アプリケーションを呼び出す必要があります[ **SetupCloseInfFile** ](https://msdn.microsoft.com/library/windows/desktop/aa376985)呼び出し中に割り当てられているリソースを解放する[ **SetupOpenInfFile**](https://msdn.microsoft.com/library/windows/desktop/aa377409)します。

 

 





