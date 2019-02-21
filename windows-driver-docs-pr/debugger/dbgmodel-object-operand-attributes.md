---
title: デバッガーのデータ モデル - オペランドのオブジェクトを属性します。
description: マシン語命令のオペランドは、オペランドの属性オブジェクトによって記述されます。
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5d8cd8b7a0915f07de8fb5748aee06ab3afbc5d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558075"
---
# <a name="operand-attributes-objects"></a>オペランドのオブジェクトを属性します。 
## <a name="summary"></a>概要
マシン語命令のオペランドは、オペランドの属性オブジェクトによって記述されます。
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|HasImmediate|オペランドの一部として、イミディ エイト値のオペランドを持つかどうかを示します。|
|IsInput|オペランドが、命令 (は、命令の内容への入力) 用のデータ ソースであるかどうかを示します。|
|IsOutput|オペランドが命令 (命令が実行する任意の出力) のデータの変換先であるかどうかを示します。|
|IsMemoryReference|オペランドがメモリの参照であるかどうかを示します。|
|IsImmediate|オペランドが、イミディ エイト値であるかどうかを示します。 このようなオペランドがあります*HasImmediate*を true に設定します。|
|IsRegister|オペランドは、レジスタでは単純にするかどうかを示します。|