---
title: ドライバー パッケージのテスト署名カタログ ファイルを作成します。
description: ドライバー パッケージのテスト署名カタログ ファイルを作成します。
ms.assetid: 0bbb4dfa-d203-4618-946e-95d2896081ac
keywords:
- テスト署名ドライバー パッケージ WDK、カタログ ファイル
- カタログ ファイル WDK ドライバー署名を作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42b77d0715a981ffdfa69518f087f55420f4f6fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550358"
---
# <a name="creating-a-catalog-file-for-test-signing-a-driver-package"></a>ドライバー パッケージのテスト署名カタログ ファイルを作成します。


カタログ (*.cat*) ファイルに含まれるすべてのファイルのデジタル署名が含まれていますの[ドライバー パッケージ](driver-packages.md)します。 詳細については、次を参照してください。[カタログ ファイル](catalog-files.md)します。

作成する 2 つの方法がある、[カタログ ファイル](catalog-files.md):

-   INF ファイルを使用して、ドライバー パッケージがインストールされている場合は、使用、 [ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)カタログ ファイルを作成するためのツール。 Inf2Cat には、パッケージの INF ファイル内で参照される、ドライバー パッケージ内のすべてのファイルに自動的に含まれています。 Inf2Cat ツールを使用する方法の詳細については、次を参照してください。[カタログ ファイルを作成するのを使用して Inf2Cat](using-inf2cat-to-create-a-catalog-file.md)します。

-   INF ファイルで、ドライバー パッケージがインストールされていない場合は、使用、 [MakeCat](https://go.microsoft.com/fwlink/p/?linkid=104922)カタログ ファイルを手動で作成されたカタログ定義ファイルを使用して作成するためのツール (*.cdf*)。

    たとえば、アプリケーションを通じて、ドライバー パッケージがインストールされている、場合、ドライバーと任意のサポートなど、パッケージのカーネル モード バイナリのすべてのコンポーネントにデジタル署名カタログ ファイルを作成する *.dll*ファイル。 MakeCat ツールを使用する方法の詳細については、次を参照してください。[カタログ ファイルを作成するのを使用して MakeCat](using-makecat-to-create-a-catalog-file.md)します。

カタログ ファイルは、次の種類のドライバーをインストールする必要はありません。

-   A*ブート開始ドライバー*します。

-   使用しないアプリケーションを使用してインストールされているドライバー、[カタログ ファイル](catalog-files.md)します。

ドライバーのこれらの型を埋め込む必要があります、ドライバー内でのデジタル署名します。 この手順の詳細については、次を参照してください。[テスト署名ドライバーは、埋め込みの署名](test-signing-a-driver-through-an-embedded-signature.md)します。

カタログ ファイルを作成する方法の詳細については、次を参照してください。 [Test-Signed ドライバー パッケージのカタログ ファイルを作成する](creating-a-catalog-file-for-a-test-signed-driver-package.md)します。

 

 





