---
title: 標準の拡散光を環境マッピング
description: 標準の拡散光を環境マッピング
ms.assetid: 7cdba0db-fdaf-46a4-a5f9-c5e930f68314
keywords:
- マッピングのキューブの環境
- 環境の WDK Direct3D のマッピング
- キューブ環境マップ WDK Direct3D
- 照明 WDK Direct3D
- 拡散光の WDK Direct3D
- 標準の拡散光 WDK Direct3D
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 8f92b2945d89652fec2d35f323020a579cb6d998
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532462"
---
# <a name="environment-mapping-with-standard-diffuse-lighting"></a>標準の拡散光を環境マッピング

ジオメトリのパイプラインでは、拡散のコンポーネントのグーロー シェーディングの拡散光の標準的な計算を実行できます。 ただし、最適なよりリアルは、反射コンポーネントをキューブ環境マッピングによって生成できます。 操作では、両方がの場合、 [FVF](fvf--flexible-vertex-format-.md)で指定されたアプリケーションは、照明の計算の位置に 1 つのベクトルを含める必要があり、キューブ マップにベクトルとして使用する個別の 3D テクスチャ座標に設定します。

 

 





