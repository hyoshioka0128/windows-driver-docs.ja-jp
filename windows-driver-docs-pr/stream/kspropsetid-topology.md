---
title: KSPROPSETID\_トポロジ
description: KSPROPSETID\_トポロジ
ms.assetid: d0c51bcf-ced3-4863-9359-9fa326122262
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d802c243dc72e83b5f57efc37306eef529a751c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341820"
---
# <a name="kspropsetidtopology"></a>KSPROPSETID\_トポロジ


## <span id="ddk_kspropsetid_topology_ks"></span><span id="DDK_KSPROPSETID_TOPOLOGY_KS"></span>


クライアント要求を使用して、KSPROPSETID で\_KS フィルターの内部のトポロジを検査するためにトポロジのプロパティが設定されます。

トポロジ内の各ノードでは、0 から始まるノード ID があります。フィルター処理 KS *n*ノード番号 0 ~ *n-1*します。 全体、KS フィルター自体のノードとして扱うことができ、特殊なノード ID を持つ番号 KSFILTER\_ノード。

Stream ミニドライバーは、このプロパティ セット内のプロパティを処理する必要はありません。 ストリーム クラス ドライバーは、ミニドライバーに代わってそれらを処理します。

Microsoft は、フォーム KSNODETYPE のノード型の標準セットを定義します。\_で XXX、 *ksmedia.h*ヘッダー ファイル。 このセットのプロパティを使用して、クライアントはこのシーケンス内の 0 から始まるインデックスでノードに参照します。

KSPROPSETID\_トポロジ プロパティ セットが含まれます。

[**KSPROPERTY\_トポロジ\_カテゴリ**](ksproperty-topology-categories.md)

[**KSPROPERTY\_トポロジ\_接続**](ksproperty-topology-connections.md)

[**KSPROPERTY\_トポロジ\_名**](ksproperty-topology-name.md)

[**KSPROPERTY\_トポロジ\_ノード**](ksproperty-topology-nodes.md)

 

 





