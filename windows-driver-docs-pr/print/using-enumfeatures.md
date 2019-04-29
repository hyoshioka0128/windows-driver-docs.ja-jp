---
title: EnumFeatures の使用
description: EnumFeatures の使用
ms.assetid: 4a87cedf-066a-445b-ad3e-71699c9d3e07
keywords:
- EnumFeatures
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91e0ec6a79b5bd380a8a01cf6d0027bf5654adaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330308"
---
# <a name="using-enumfeatures"></a>EnumFeatures の使用





呼び出し元を使用できる**EnumFeatures**キーワードを取得する一覧を含む現在サポートされているドライバーの機能と PPD のすべての機能をさらに Pscript 場合 PPD内で定義されている機能と同様の処理を次に\*OpenUI/\*CloseUI 構造キーワード。

\*LeadingEdge

\*UseHWMargins

Pscript は、特別な方法で、特定の機能を処理します。 1 つ以上の場合\*解像度、 \*SetResolution、および\*JCLResolution キーワード標準機能の 1 つにマージされます PPD に表示されます。 マージ後、機能のキーワード名となります"JCLResolution" \*JCLResolution 最初に表示されます。 それ以外の場合、"解決"をことができます。

**注**  ドライバーの一部の機能 (% などミラーリング) は常にサポートされて、その他のドライバーの機能は特定の条件下でのみサポートされています。 たとえば、スプーラー EMF スプールが Windows 2000 以降のオペレーティング システムで無効にした場合リリースは、%pageorder 機能はサポートされていません。 これらのドライバーがサポートされていない機能の出力キーワードの一覧に表示されません**EnumFeatures**します。

 

ドライバーの機能の出力に「%」キーワードのプレフィックスが含まれます。 PPD 機能、キーワードのプレフィックス"\*"は出力に含まれていません。

 

 




