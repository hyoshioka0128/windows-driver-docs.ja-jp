---
title: DirectX グラフィックス インフラストラクチャ DDI
description: DirectX グラフィックス インフラストラクチャ DDI
ms.assetid: e4f2bd03-d04b-4f67-94ff-54e023000f35
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0660383fe70fe1ed38af16121eddac78fc8484d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553006"
---
# <a name="directx-graphics-infrastructure-ddi"></a>DirectX グラフィックス インフラストラクチャ DDI


DirectX Graphics Infrastructure (DXGI) は、グラフィックスの一部が他よりも緩やかに変化に進化させることが判明に基づいて作成されました。 DXGI は、将来のグラフィックス コンポーネントの共通のフレームワークを提供します。 DXGI を活用した最初の Direct3D ランタイム バージョンには、Direct3D バージョン 10 です。 Direct3D のランタイムの以前のバージョンでは、低レベルのタスクへのアクセスは、Direct3D ランタイムで含まれていました。 DXGI、Direct3D ランタイムからいない共有の低レベルのタスクを個別に管理する DDI を定義します。 DXGI で、次のタスクが実装され、これらのタスクを処理するために、DXGI DDI を使用することができます。

-   プレゼンテーション

-   ガンマ補正コントロール

-   リソースの保存場所

-   リソースの優先順位

次のセクションでは、ユーザー モードのドライバー サポートを表示および DXGI DDI の使用について説明します。

[DXGI DDI をサポートしています。](supporting-the-dxgi-ddi.md)

[リソースの作成時に DXGI 情報を渡す](passing-dxgi-information-at-resource-creation-time.md)

[DXGI プレゼンテーションのパス](dxgi-presentation-path.md)

[レジストリで DXGI 情報の設定](setting-dxgi-information-in-the-registry.md)

 

 





