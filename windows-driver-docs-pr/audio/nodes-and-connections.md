---
title: ノードと接続
description: ノードと接続
ms.assetid: 829b1067-8246-49fc-94f1-4988e61defac
keywords:
- オーディオは、WDK のオーディオ、ノードをフィルター処理します。
- オーディオは WDK にオーディオ、接続をフィルター処理します。
- オーディオのトポロジ ノード WDK
- トポロジ ノードの WDK オーディオ
- 接続の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c36bec2f88a313cab41fcd8cbebfd25e3b619066
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558828"
---
# <a name="nodes-and-connections"></a>ノードと接続


## <span id="nodes_and_connections"></span><span id="NODES_AND_CONNECTIONS"></span>


フィルター ノードの記述子の配列の形式では、そのトポロジ ノードの説明を提供します ([**PCNODE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537720)構造)。 配列内の各記述子が 1 つのノードについて説明し、ノードの種類を指定する GUID が含まれています (たとえば、 [ **KSNODETYPE\_リバーブ**](https://msdn.microsoft.com/library/windows/hardware/ff537189))。 オーディオ デバイスに対して定義されている標準的なノードの種類の一覧は、[オーディオ トポロジ ノード](https://msdn.microsoft.com/library/windows/hardware/ff536219)を参照してください。

フィルターは、記述子の配列内のノードのインデックスを使用してそのノードのそれぞれを識別します。 たとえばをフィルターまたはフィルターで特定のピンには、特定のノード プロパティの要求を送信するとき、クライアントにはによって、ターゲット ノードを識別するために、要求でノードの ID (配列のインデックス) が含まれます。

フィルターは接続記述子の配列の形式で内部接続の説明を示します ([**PCCONNECTION\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff537688)構造)。 各記述子では、フィルターの内部接続のいずれかについて説明します。 記述子は、pin とノード間の接続または 2 つのノード間の接続について説明しますか。

ノードと、フィルターが一緒に公開する接続は、フィルターの内部のトポロジを定義します。 トポロジ、オーディオ デバイスの内部レイアウトのマップは、それが表すハードウェアの組織を正確に反映する必要があります。 Microsoft Windows のマルチ メディア ミキサー API は、たとえば、ミキサーの行に、フィルターの内部接続およびミキサーの行をコントロールには、そのノードに変換 (を参照してください[オーディオ Mixer API 翻訳にカーネル ストリーミング トポロジ](kernel-streaming-topology-to-audio-mixer-api-translation.md))。 フィルターの内部のトポロジの間違いは、ミキサー行表現に反映され、ミキサー API を使用するアプリケーションでエラーや予期しない動作を引き起こす可能性があります。

 

 




