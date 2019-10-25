---
title: ノードと接続
description: ノードと接続
ms.assetid: 829b1067-8246-49fc-94f1-4988e61defac
keywords:
- オーディオフィルター WDK オーディオ、ノード
- オーディオフィルター WDK オーディオ、接続
- オーディオトポロジノード WDK
- トポロジノード WDK オーディオ
- WDK オーディオの接続
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11eef7490ba213800714e50bcc355873772993f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830349"
---
# <a name="nodes-and-connections"></a>ノードと接続


## <span id="nodes_and_connections"></span><span id="NODES_AND_CONNECTIONS"></span>


このフィルターは、ノード記述子の配列 ([**Pcnode\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcnode_descriptor)構造) の形式で、そのトポロジノードの説明を提供します。 配列内の各記述子は、1つのノードを表し、ノードの種類を指定する GUID を含んでいます (たとえば、 [**KSNODETYPE\_リバーブ**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-reverb))。 オーディオデバイスに対して定義されている標準のノードの種類の一覧については、「[オーディオトポロジノード](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-topology-nodes)」を参照してください。

フィルターは、記述子配列内のノードのインデックスによって、各ノードを識別します。 たとえば、フィルターまたはフィルターの特定のピンにノード固有のプロパティ要求を送信する場合、クライアントはターゲットノードを識別するために、要求にノード ID (配列インデックス) を含めます。

このフィルターは、接続記述子の配列 ([**pcconnection\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))構造) の形式で内部接続の説明を提供します。 各記述子は、フィルターの内部接続の1つを記述します。 記述子は、ピンとノード間の接続、または2つのノード間の接続を表すことができます。

フィルターによって公開されるノードと接続は、フィルターの内部トポロジを定義します。 トポロジは、オーディオデバイスの内部レイアウトのマップであり、それが表すハードウェアの編成を正確に反映している必要があります。 たとえば、Microsoft Windows マルチメディアミキサー API は、フィルターの内部接続をミキサーラインとそのノードに変換し、ミキサーライン上のコントロールに変換します (「[カーネルストリーミングトポロジからオーディオミキサー API への変換](kernel-streaming-topology-to-audio-mixer-api-translation.md)」を参照してください)。 フィルターの内部トポロジにおける不正確な結果は、ミキサーライン表現に反映され、ミキサー API を使用するアプリケーションでエラーや予期しない動作が発生する可能性があります。

 

 




