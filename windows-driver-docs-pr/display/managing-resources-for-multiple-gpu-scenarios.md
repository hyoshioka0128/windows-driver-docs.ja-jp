---
title: 複数の GPU シナリオに対するリソースの管理
description: 複数の GPU シナリオに対するリソースの管理
ms.assetid: f3dc10b1-76e9-4f31-b253-149b6300611d
keywords:
- GPU WDK Windows 7 の表示
- 複数の GPU WDK Windows 7 の表示
- GPU WDK Windows 7 の表示、複数のリソースの管理
- 複数の Gpu WDK Windows 7 の表示
- リソースの管理、Gpu WDK Windows 7 の複数の表示
- GPU WDK Windows 2008 のリソース R2 の表示
- 複数の GPU WDK Windows 2008 のリソース R2 の表示
- GPU WDK Windows 2008 のリソース R2 の表示、複数のリソースの管理
- Gpu WDK Windows 2008 のリソース R2 の複数の表示
- リソースの管理、Gpu WDK Windows 2008 のリソース R2 の複数の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7185420264d2114b6b4a3a94054d076adfa4c03d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379861"
---
# <a name="managing-resources-for-multiple-gpu-scenarios"></a>複数の GPU シナリオに対するリソースの管理


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

複数の GPU シナリオ用のリソースを適切に管理するには、ユーザー モードのディスプレイ ドライバーは、新しいデバイス ドライバー インターフェイス (DDI) Windows 7 に付属するを実装できます。 各リソースを表示するために複数の Gpu のメモリの間で分割できます。 ドライバーは、新しいリソースの所有者があるマージされたリソースを持つように各リソースを再マージするこの新しい DDI を実装できます。 この DDI 実装では、ドライバーは、リソースが変更されるすべての部分的に構築されたコマンド バッファーをフラッシュする必要があります。 この DDI が拡張機能として提供される、 [Direct3D のバージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)および、 [Direct3D のバージョン 10 DXGI DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 ドライバーを実装できます[ **ResolveSharedResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_resolvesharedresource)サポート Microsoft Direct3D 機能レベル 9 と[ **ResolveSharedResourceDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions)Direct3D 機能レベル 10 と 11 をサポートします。

Windows 8.1 以降、ユーザー モード ドライバーは独立した GPU と統合された GPU の間で共有されるクロス アダプターのリソースをサポートできます。 参照してください[ハイブリッド システムでクロス アダプターのリソースを使用して](using-cross-adapter-resources-in-a-hybrid-system.md)します。

 

 





