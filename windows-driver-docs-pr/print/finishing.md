---
title: 終了
description: 終了
ms.assetid: 5c8e556b-102a-4caf-92d3-8b61bec1a29f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87c48599392268cb6ff9fdd8be68c9a43ab813a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551028"
---
# <a name="finishing"></a>終了


スキーマのパス:\\Printer.Finishing

ノード型: プロパティ

最後のプロパティには、印刷が完了した後に実行された操作に関するデータが含まれています。 これは、ホチキス止め、ドキュメントを照合できるかどうかが含まれます。 使用可能な出力ビンに関する情報と共に、穴のパンチします。

最後のプロパティには、CollationSupported と JogOffsetSupported; で、子の値が 2 つが含まれています。親であることも、[ホチキス止め](staple3.md)、 [HolePunch](holepunch3.md)、および[OutputBins](outputbins2.md)プロパティ。

### <a name="span-idcollationsupportedspanspan-idcollationsupportedspan-collationsupported"></a><span id="collationsupported"></span><span id="COLLATIONSUPPORTED"></span> CollationSupported

スキーマのパス:\\Printer.Finishing:CollationSupported

ノード型: 値

データ型: BIDI\_BOOL

説明: プリンターが印刷されるドキュメントのハードウェアの照合順序をサポートしているかどうかを示します。 場合**TRUE**、照合順序がサポートされています。 場合**FALSE**、照合順序はサポートされていません。

### <a name="span-idjogoffsetsupportedspanspan-idjogoffsetsupportedspan-jogoffsetsupported"></a><span id="jogoffsetsupported"></span><span id="JOGOFFSETSUPPORTED"></span> JogOffsetSupported

スキーマのパス:\\Printer.Finishing:JogOffsetSupported

ノード型: 値

データ型: BIDI\_BOOL

説明: プリンターが時差のグループで出力トレイ内の印刷ジョブまたは別の印刷ジョブの別のコピーを配置をサポートしているかどうかを決定します。 場合**TRUE**場合、プリンターがジョブのオフセットをサポートして**FALSE**プリンターはこの機能をサポートしていません。

 

 




