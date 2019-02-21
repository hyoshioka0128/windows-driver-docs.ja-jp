---
title: セグメント化フィルターの実装に関するメモ
description: セグメント化フィルターの実装に関するメモ
ms.assetid: c4caf8dd-8108-4bc7-b02f-1e180fedb95f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d8011470161b6796ff61a25e48530e4f0e8b048
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538869"
---
# <a name="implementation-notes-for-segmentation-filters"></a>セグメント化フィルターの実装に関するメモ





各子項目の作成にセグメント化フィルターを設定するプロパティをメモに重要です。 次のプロパティがあります。[**WIA\_IP\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)、 [ **WIA\_IP\_YPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552671)、 [ **WIA\_IP\_XEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552661)、WIA\_IP\_YEXTENT、および場合によって[ **WIA\_IP\_DESKEW\_X** ](https://msdn.microsoft.com/library/windows/hardware/ff552581)と[ **WIA\_IP\_DESKEW\_Y**](https://msdn.microsoft.com/library/windows/hardware/ff552587)します。 これらのプロパティ値に渡されたイメージではなく、ベッドでアイテムの位置に対応して、 *pInputStream*パラメーター。

したがっては、WIA に細心の注意をセグメント化フィルターの重要な\_IP\_XPOS、WIA\_IP\_YPOS、および[ **WIA\_IP\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff552648)渡されたイメージのプロパティ。

例としてには、アプリケーションではプレビューのスキャンは WIA が設定されると仮定\_IP\_XPOS WIA を =\_IP\_YPOS (親) の項目にプレビュー イメージを取得する前に 200 を = です。 これは、後地区のことを検出するために、セグメント化フィルターへの呼び出しで。 ただし、セグメント化フィルターで使用される実際のアルゴリズムでは、そこに渡されるイメージでは機能します。 このアルゴリズムでは、イメージの左端と 200 ピクセル下の右側に地区のコーナー 150 ピクセルを検出した、イメージの上から場合、これ実際には対応にあるポイントに (350, 400)、スキャナーにします。

次の図では、外側の領域は、フラット ベッド スキャナーを表します。 アルゴリズムがある領域の左上隅の座標を検索 (150, 200) の値をセグメント化フィルターする必要があります設定を子項目に wia\_IP\_XPOS と WIA\_IP\_YPOS 350、400 です。

![セグメント化フィルターからプラテン上の部分に適用されたを示す図](images/art-segmentation3.png)

たとえば、アプリケーションで表示する場合、セグメント化フィルターによって視覚的に検出されたリージョンは、セグメント化フィルターが、フラット ベッド内の位置に対応する座標を設定することに注意してください場合があります。 つまり、アプリケーションが、プレビュー イメージの座標にベッドの座標をマップする必要があります。 ほとんどの場合、ただし、アプリケーションは、WIA を使用してプレビュー スキャン\_IP\_XPOS = WIA\_IP\_YPOS = 0 および回転のない ([**WIA\_IP\_回転**](https://msdn.microsoft.com/library/windows/hardware/ff552648) = 縦向き)。 大文字と小文字の場合は、フラット ベッドの座標とプレビュー イメージの間の直接マッピングがあります。

セグメント化フィルターする必要がありますに注意を払うもう 1 つのプロパティは、回転プロパティ、WIA\_IP\_回転、ドライバーは、このプロパティを実装を提供します。 たとえばにプレビュー イメージを取得する際に、アプリケーションが WIA が設定されると仮定\_IP\_ROT180 に回転します。 ここで実際にセグメント化、フィルターに渡されるイメージの左上隅にあるが、ベッドの右下隅に対応します。 そのため、セグメント化、フィルターは、フラット ベッドに座標を回転したイメージで検出した各サブ領域の座標をマップする必要があります。 WIA を設定できますが、セグメント化フィルターがこのマッピングを実行すると、\_IP\_XPOS、WIA\_IP\_YPOS、および他のプロパティの値に、子項目、サブイメージに対応します。

ほとんどの場合、WIA に注意してください、\_IP\_XPOS と WIA\_IP\_YPOS WIA ゼロに設定されます\_IP\_回転は縦に設定されます。 ただし、セグメント化で設定されていないこれらの値にケースを処理できる必要があります。

アプリケーションは、イメージのドライバーが回転されたセグメント化のフィルターに渡すことができますに渡す必要があるないをデスキューが既に実行されて、イメージにも注意してください。

 

 




