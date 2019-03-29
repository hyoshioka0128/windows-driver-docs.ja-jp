---
title: ファイルへのアクセスおよび変更
description: ファイルへのアクセスおよび変更
ms.assetid: DD5A527F-5F8D-4892-A2D5-C0279913B6A3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f18a1da45c2fe994992ac92768ef14435123de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579964"
---
# <a name="accessing-and-modifying-files"></a>ファイルへのアクセスおよび変更


次のガイドラインは、アクセスまたはファイルを変更したときに、ドライバー パッケージのコンポーネントに適用されます。

-   のみを使用してファイルを変更する必要があります[INF ディレクティブ](inf-directives.md)INF ファイル内で。 など、INF を使用して、 [ **CopyFiles** ](inf-copyfiles-directive.md)ファイルと、INF をコピーするディレクティブ[ **RenFiles** ](inf-renfiles-directive.md)ディレクティブ ファイルの名前を変更します。

-   INF に表示されるファイル[ **CopyFiles** ](inf-copyfiles-directive.md)ディレクティブが、INF にも表示する必要がありますされません[ **RenFiles** ](inf-renfiles-directive.md)または[ **DelFiles** ](inf-delfiles-directive.md) INF ファイルでディレクティブ。

**重要な**  、INF [ **RenFiles** ](inf-renfiles-directive.md)と[ **DelFiles** ](inf-delfiles-directive.md)ディレクティブを慎重に使用する必要があります。 必要がありますいないドライバーを使用する INF ファイルでこれらのディレクティブのプラグ アンド プレイ (PnP) 関数。

 

 

 





