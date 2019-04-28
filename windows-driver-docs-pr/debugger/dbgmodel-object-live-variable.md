---
title: Debugger Data Model - ライブ変数オブジェクト
description: その特定の命令にライブであるし、配置されている場所の変数に関する情報のコレクション
ms.date: 12/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: c228ccd00d97693462a94e6f96589513e889e7b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376080"
---
# <a name="live-variable-objects"></a>ライブ オブジェクト変数 
## <a name="summary"></a>概要
完全なシンボリック情報を使用する場合、それぞれの命令には、その特定の命令にライブであるし、配置されている場所の変数に関する情報のコレクションが含まれています。
## <a name="object-properties"></a>オブジェクトのプロパティ
|名前|説明|
|--- |--- |
|LocationKind|内で変数が格納されている場所の種類を説明する文字列 (例。"Register"、"RegisterRelative"など..)。|
|Offset|変数が格納されている場所からのオフセット。 たとえば [rbp + 8] に格納されている変数、オフセットは 8 になります。|
|登録する|A[登録](dbgmodel-object-register.md)を基準とする、変数の格納場所またはレジスタを記述するオブジェクト。|
|VariableName|これについては説明されている変数の名前。|