---
title: Debugger Data Model - 命令属性オブジェクト
description: 一部の命令の詳細の説明が含まれています。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8687a5eb0606fe7c633f5b7e6e1ad5ff0303e5c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373413"
---
# <a name="instruction-attributes-objects"></a>命令のオブジェクトを属性します。 
## <a name="summary"></a>概要
*属性*のプロパティ、[命令](dbgmodel-object-instruction.md)オブジェクトには、一部の命令の詳細の説明が含まれています。
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|IsBranch|命令が分岐命令の任意の並べ替えであるかどうかを示します。|
|IsConditional|命令の結果が条件付きかどうかを示します (例: 条件付き分岐)。|
|IsCall|命令がなんらかの呼び出し命令であるかどうかを示します。|
|IsReturn|命令が戻り命令の任意の並べ替えであるかどうかを示します。|