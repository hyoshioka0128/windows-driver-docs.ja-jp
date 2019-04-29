---
title: KSPROPSETID\_Hrtf3d
description: KSPROPSETID\_Hrtf3d
ms.assetid: 8045991b-0409-445a-bd35-d9b8644f770e
keywords:
- KSPROPSETID_Hrtf3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd94c3b3916952d762fc25583159057164b4008
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332512"
---
# <a name="kspropsetidhrtf3d"></a>KSPROPSETID\_Hrtf3d


## <span id="ddk_kspropsetid_hrtf3d_ks"></span><span id="DDK_KSPROPSETID_HRTF3D_KS"></span>


`KSPROPSETID_Hrtf3d`プロパティ セットは DirectSound バッファーの 3D の head 相対転送関数 (HRTF) を構成するために使用します。 このセットには、3 D のノードの省略可能なプロパティが含まれています ([**KSNODETYPE\_3D\_効果**](ksnodetype-3d-effects.md)) DirectSound 暗証番号 (pin) のインスタンスにします。

3D のすべてのノードでは、HRTF 処理をサポートします。 クライアントは、そのノードが HRTF 処理を実行できるかどうかを判断する 3D ノードに HRTF プロパティの基本サポート クエリを送信できます。 3D のノードをサポートする、`KSPROPSETID_Hrtf3d`プロパティ セットは、セット内のプロパティの 3 つすべてをサポートする必要があります。

このプロパティ セットの定義では、無限インパルス応答 (IIR) フィルターの 1 つの位置にあるオーディオ ソースの効果を表すと HRTF アルゴリズムを実装することを前提としています。

通常、デジタル フィルターには、最初の一時的な応答があります。 フィルター係数を変更する 1 つの位置から、次に、ソースを移動する場合と HRTF アルゴリズム クロス フェード、出力は、元の位置にあるフィルターから新しい位置にあるフィルター。 **FilterTransientMuteLength**のメンバー、 [ **KSDS3D\_HRTF\_INIT\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff537106)構造体の数を指定します。遅延の間に使用するサンプルは、新しいフィルターの初期の一時的なレンダリングを回避するためにフェードインします。 この期間中、出力は、古いフィルターのみから取得されます。 **FilterOverlapBufferLength**メンバー (同じ構造体) をミュートする対象となるサンプルの合計数を指定し、クロス フェード フィルターを出力します。

ソースは、右の半平面から左に移動、ときに、フィルターに切り替えます。 このスイッチは、音の pop にあります。 **SwapChannels**のメンバー、 [ **KSDS3D\_HRTF\_PARAMS\_MSG** ](https://msdn.microsoft.com/library/windows/hardware/ff537108)構造体をスワップする HRTF アルゴリズムに指示しますその他の半分の平面にソースの場所を逆に出力します。 **CrossFadeOutput**メンバー (同じ構造体) をクロス フェード出力チャネル方位角の間で遷移を角度 0 の後にアルゴリズムに指示します。 **OutputOverlapBufferLength** KSDS3D のメンバー\_HRTF\_INIT\_メッセージをこの遷移の発生時にクロス フェードする対象となるサンプルの数を指定します。

対称性のためには、方位角角度が 0 の場合、HRTF アルゴリズムにダウンロードするフィルターの係数の半分だけ必要があります。 **ZeroAzimuth** KSDS3D のメンバー\_HRTF\_PARAMS\_メッセージは、この条件が発生することを示します。

HTRF DirectSound API での処理を構成する方法の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

`KSPROPSETID_Hrtf3d`プロパティ セットには、次の 3 つのメンバーが含まれています。

[**KSPROPERTY\_HRTF3D\_フィルター\_形式**](ksproperty-hrtf3d-filter-format.md)

[**KSPROPERTY\_HRTF3D\_初期化**](ksproperty-hrtf3d-initialize.md)

[**KSPROPERTY\_HRTF3D\_PARAMS**](ksproperty-hrtf3d-params.md)

 

 





