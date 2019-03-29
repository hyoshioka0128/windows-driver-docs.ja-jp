---
title: HTTP サイトと UNC 共有
description: HTTP サイトと UNC 共有
ms.assetid: a1b79242-41ba-4c95-89fd-dbb7f70b24eb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10446bc395970f4998593182340ea9b4089484da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578389"
---
# <a name="http-sites-and-unc-shares"></a>HTTP サイトと UNC 共有


SrcSrv を使用して WinDbg をバージョン固有のソースを提供する Web サイトを設定することになります。 このようなメカニズムが、バージョン管理からのソース ファイルの動的な抽出を提供しませんから多くのモジュールのバージョンの多くのソースを提供する 1 つの統一されたパスに WinDbg のソース パスを設定できるため、これは役に立つの機能、デバッグ シナリオごとに個別のパスを設定する代わりにします。 これは、実際のバージョン コントロール システムに直接アクセスができるソース リモートの場所からをセキュリティで保護された HTTP ベースのアクセスを提供する相手の支援のデバッグのクライアントに関係のないです。 対象の Web サイトは、必要な場合は、HTTPS やスマート カードをにより保護できます。 単純な UNC 共有を使用してソース ファイルを提供する、この同じ手法を使用できます。

このセクションの内容:

[Web サイトを設定します。](setting-up-the-web-site.md)

[ソース ファイルを抽出します。](extracting-source-files.md)

[.Pdb ファイル内のストリームをインデックス作成のソースの変更](modifying-the-source-indexing-streams-in-a--pdb-file.md)

[UNC 共有を使用](using-unc-shares.md)

[標準バージョン コントロールに合わせて HTTP サイトと UNC 共有を使用します。](using-http-sites-and-unc-shares-in-conjuction-with-regular-version-con.md)

 

 





