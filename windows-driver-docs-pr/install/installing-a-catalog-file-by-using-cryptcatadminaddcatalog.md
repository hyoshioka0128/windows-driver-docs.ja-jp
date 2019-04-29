---
title: CryptCATAdminAddCatalog を使用したカタログ ファイルのインストール
description: CryptCATAdminAddCatalog を使用したカタログ ファイルのインストール
ms.assetid: 2ab71f74-5a94-4f07-bd08-d3f5f6b6a785
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 446055e4774094b72d8c2f7fce96c5c324f444d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325284"
---
# <a name="installing-a-catalog-file-by-using-cryptcatadminaddcatalog"></a>CryptCATAdminAddCatalog を使用したカタログ ファイルのインストール


インストール プログラムを使用できる、 [CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=104926)およびその他の**CryptCATAdmin * Xxx*** インストール プログラムを使用する暗号化関数、[カタログ ファイル](catalog-files.md)システムのコンポーネントおよびドライバー データベース。

インストール プログラムは、次のように、Windows 7 および .NET Framework 4.0 用 Microsoft Windows ソフトウェア開発キット (SDK) を使用する必要があります。

- インストール プログラムのソース ファイルは、次のヘッダーを含める必要があります (*.h*) ファイル。
  - *Mscat.h*、様々 なプロトタイプと構造を定義する**CryptCATAdmin * Xxx*** 関数。
  - *Softpub.h*、さまざまなデータ構造とで使用される Guid を定義する、 **CryptCATAdmin * Xxx*** 関数。

- インストール プログラムにリンクする必要があります*Wintrust.lib*します。

これらを使用する**CryptCATAdmin * Xxx*** 暗号化機能、インストール プログラムは、次を実行します。

1.  呼び出し[CryptCATAdminAcquireContext](https://go.microsoft.com/fwlink/p/?linkid=105783)カタログ管理者のコンテキストを識別するハンドルを取得します。 アプリケーションを設定して、サブシステムの識別、 *pgSubsystem* GUID DRIVER_ACTION_VERIFY へのポインターへの入力パラメーター。 この GUID がで定義されている*Softpub.h*します。

2.  呼び出し[CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=136382)を追加する、[カタログ ファイル](catalog-files.md)システム コンポーネントおよびドライバー データベースにします。 インストール プログラムは手順 1、カタログ ファイルの完全修飾パスへのポインターと関数を使用してカタログ fi のコピーをインストールするカタログ ファイルの名前へのポインターで取得したカタログ管理者のコンテキストを識別するハンドルを提供します。データベースで le です。 関数は、データベースに追加されたカタログ ファイルのカタログ情報のコンテキストへのハンドルを返します。

3.  呼び出し[CryptCATAdminReleaseCatalogContext](https://go.microsoft.com/fwlink/p/?linkid=105784)カタログ ファイルのカタログ情報のコンテキストを識別するハンドルを解放します。 インストール プログラムは、手順 1. で取得した、カタログ管理者コンテキストを識別するハンドルと手順 2. で返されたカタログ情報のコンテキストを識別するハンドルを提供します。

4.  呼び出し[CryptCATAdminReleaseContext](https://go.microsoft.com/fwlink/p/?linkid=105785)カタログ管理者のコンテキストを識別するハンドルを解放します。 アプリケーションでは、手順 1. で取得した、カタログ管理者コンテキストを識別するハンドルを提供します。









