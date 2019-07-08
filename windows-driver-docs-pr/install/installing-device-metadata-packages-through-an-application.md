---
title: アプリケーションからのデバイス メタデータ パッケージのインストール
description: アプリケーションからのデバイス メタデータ パッケージのインストール
ms.assetid: 3fec5938-b81b-4efe-8bcd-b2ef4b1c4b8b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d522b4f759455843b774385cf6781a359880d70d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369461"
---
# <a name="installing-device-metadata-packages-through-an-application"></a>アプリケーションからのデバイス メタデータ パッケージのインストール


デバイス メタデータ パッケージをインストールする、[デバイス メタデータ ストア](device-metadata-store.md)デバイスのインストール アプリケーションなど、アプリケーションを使用してこれらの手順に従います。

1.  アプリケーションが最初のパスを検索、[デバイス メタデータ ストア](device-metadata-store.md)呼び出すことによって、 [SHGetKnownFolderPath](https://go.microsoft.com/fwlink/p/?linkid=145428)関数。 [KNOWNFOLDERID](https://go.microsoft.com/fwlink/p/?linkid=145429)デバイスのメタデータ ストアの GUID は {5CE4A5E9-E4EB-479D-B89F-130C02886155}。

2.  次に、アプリケーション、デバイスのメタデータ ストアに呼び出すことによって、デバイス メタデータ パッケージをコピーする、 [CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596)関数。

    **注**アプリケーションは、管理者特権でコマンド プロンプト ウィンドウから管理者特権で実行中または開始をする必要があります。



アプリケーションがデバイス メタデータ パッケージをコピーするとき、[デバイス メタデータ ストア](device-metadata-store.md)、次の手順を完了する必要があります。

1.  デバイス メタデータ パッケージのロケールのデバイスのメタデータ ストアのサブディレクトリが存在しない場合、アプリケーションは、ターゲット ロケールの名前を使用して、サブディレクトリを作成する必要があります。

    たとえば、パッケージのロケールが EN-US の場合は、アプリケーション作成する必要があります、 *EN-US*サブディレクトリが現在存在しない場合は、デバイス メタデータのストアのパスの下のサブディレクトリ。

2.  デバイス メタデータ パッケージのコピーを適切な *&lt;ロケール&gt;* 内のサブディレクトリ、[デバイス メタデータ ストア](device-metadata-store.md)します。

    **注**を使用する場合、 [CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596)デバイス メタデータ パッケージのコピーで、適切なを含む完全なパス名を指定する関数 *&lt;ロケール&gt;* サブディレクトリです。 この手順を実行して[CopyFile]( https://go.microsoft.com/fwlink/p/?linkid=189596)ローカル コンピューターに存在しない場合は、パッケージに関連付けられているサブディレクトリを作成します。




デバイス後メタデータ パッケージがインストールされている、[デバイス メタデータ ストア](device-metadata-store.md)、[デバイス メタデータの取得クライアント](device-metadata-retrieval-client.md)(DMRC) は、デバイス メタデータ パッケージにアクセスし、デバイス情報を表示しますデバイスとプリンターのユーザー インターフェイス。










