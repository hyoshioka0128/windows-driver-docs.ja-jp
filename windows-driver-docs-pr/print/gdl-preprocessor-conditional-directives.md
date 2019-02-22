---
title: GDL プリプロセッサ条件付きディレクティブ
description: GDL プリプロセッサ条件付きディレクティブ
ms.assetid: 5eb4bcbf-3f5e-44cc-b4e5-716a15e43b15
keywords:
- WDK GDL、ソース ファイルのプリプロセッサ ディレクティブのディレクティブ
- ソース ファイル WDK GDL、プリプロセッサ ディレクティブ
- プリプロセッサ ディレクティブ WDK GDL、条件付きディレクティブ
- WDK GDL、条件付きディレクティブのディレクティブ
- 条件付きディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 508e588296219506421258d73e1f10200cc8553f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549412"
---
# <a name="gdl-preprocessor-conditional-directives"></a>GDL プリプロセッサ条件付きディレクティブ


GDL プリプロセッサ条件付きディレクティブは、条件構造を定義します。 各条件付きコンストラクトが始まり、  **\#Ifdef**ディレクティブで終了し、  **\#Endif**ディレクティブ。 間に、  **\#Elseifdef**ディレクティブには、0 が表示される、1 つ以上の時間。 省略可能な **\#Else**ディレクティブは、最後の間で記述する必要があります **\#Elseifdef**ディレクティブ (存在する場合に使用) と、最終的な **\#Endif**ディレクティブ。

中間のデータ (非プリプロセッサ ディレクティブ) を条件付きセクションにこれらのディレクティブの各パーティションします。各セクションは解析の次のステージの保持または以下に示すようにプリプロセス時に削除します。 処理がないとしない任意の条件構造内に含まれるデータは常に保持されます。

条件付きセクション ディレクティブは入れ子にできます。 全体の条件付きコンストラクト、  **\#Ifdef**終了に **\#Endif**全体、それを囲む条件付きコンストラクトの 1 つのセクション内に存在する必要があります。

GDL では、次の条件付きディレクティブを使用します。

[\#Ifdef](-ifdef-conditional-preprocessor-directive.md)

[\#Elseifdef](-elseifdef-conditional-preprocessor-directive.md)

[\#Else](-else-conditional-preprocessor-directive.md)

[\#Endif](-endif-conditional-preprocessor-directive.md)

 

 




