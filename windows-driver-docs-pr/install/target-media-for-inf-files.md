---
title: INF ファイルのターゲット メディア
description: INF ファイルのターゲット メディア
ms.assetid: f1aaea38-e500-40a9-89c1-9c4447054fb1
keywords:
- INF ファイル WDK デバイス インストールでは、対象のメディア
- ターゲット メディア WDK INF ファイル
- WDK の INF ファイルの場所
- メディア WDK INF ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 019e858cc076734496c1d90a69be0ea69eb15d7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569782"
---
# <a name="target-media-for-inf-files"></a>INF ファイルのターゲット メディア





INF ファイルを指定したデバイスのファイルのターゲットの場所、 [ **DestinationDirs** ](inf-destinationdirs-section.md)セクション。 セクションには、コピー、名前の変更、または delete ステートメントと、このセクションでは常に同じ INF ファイルで指定する必要があります。

A **DestinationDirs**セクションを含める必要があります、 **DefaultDestDir**エントリ。

名前変更、または、削除のセクションでは、INF にコピーがある場合は、 **DestinationDirs**セクションと、INF は、その他の INF ファイルが含まれています、Windows は、ターゲットの場所の情報に含まれる INF ファイルを検索します。 ただし、Windows が含まれているファイルを検索する順序は予測できません。 そのため、Windows は、たとえば、ファイルをコピーする INF ライターではありません場所にリスクがあります。 このような混乱を避けるためには、常に指定を**DestinationDirs**セクションが含まれる INF、名前の変更、またはセクションを削除します。 **DestinationDirs**セクションに含める必要がありますが、少なくとも**DefaultDestDir**エントリをコピー、名前の変更、またはファイルを削除、INF セクションに一覧を表示できます。

 

 





