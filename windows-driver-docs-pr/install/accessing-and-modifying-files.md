---
title: ファイルへのアクセスおよび変更
description: ファイルへのアクセスおよび変更
ms.assetid: DD5A527F-5F8D-4892-A2D5-C0279913B6A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f18a1da45c2fe994992ac92768ef14435123de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375726"
---
# <a name="accessing-and-modifying-files"></a>ファイルへのアクセスおよび変更


次のガイドラインは、アクセスまたはファイルを変更したときに、ドライバー パッケージのコンポーネントに適用されます。

-   のみを使用してファイルを変更する必要があります[INF ディレクティブ](inf-directives.md)INF ファイル内で。 など、INF を使用して、 [ **CopyFiles** ](inf-copyfiles-directive.md)ファイルと、INF をコピーするディレクティブ[ **RenFiles** ](inf-renfiles-directive.md)ディレクティブ ファイルの名前を変更します。

-   INF に表示されるファイル[ **CopyFiles** ](inf-copyfiles-directive.md)ディレクティブが、INF にも表示する必要がありますされません[ **RenFiles** ](inf-renfiles-directive.md)または[ **DelFiles** ](inf-delfiles-directive.md) INF ファイルでディレクティブ。

**重要な**  、INF [ **RenFiles** ](inf-renfiles-directive.md)と[ **DelFiles** ](inf-delfiles-directive.md)ディレクティブを慎重に使用する必要があります。 必要がありますいないドライバーを使用する INF ファイルでこれらのディレクティブのプラグ アンド プレイ (PnP) 関数。

 

 

 





