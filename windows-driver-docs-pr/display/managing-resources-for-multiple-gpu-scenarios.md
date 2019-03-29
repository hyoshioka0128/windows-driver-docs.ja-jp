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
ms.openlocfilehash: d6d88283374031e92a7f367b9052f3247f43460d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580244"
---
# <a name="managing-resources-for-multiple-gpu-scenarios"></a>複数の GPU シナリオに対するリソースの管理


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

複数の GPU シナリオ用のリソースを適切に管理するには、ユーザー モードのディスプレイ ドライバーは、新しいデバイス ドライバー インターフェイス (DDI) Windows 7 に付属するを実装できます。 各リソースを表示するために複数の Gpu のメモリの間で分割できます。 ドライバーは、新しいリソースの所有者があるマージされたリソースを持つように各リソースを再マージするこの新しい DDI を実装できます。 この DDI 実装では、ドライバーは、リソースが変更されるすべての部分的に構築されたコマンド バッファーをフラッシュする必要があります。 この DDI が拡張機能として提供される、 [Direct3D のバージョン 9 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552927)および、 [Direct3D のバージョン 10 DXGI DDI](https://msdn.microsoft.com/library/windows/hardware/ff552905)します。 ドライバーを実装できます[ **ResolveSharedResource** ](https://msdn.microsoft.com/library/windows/hardware/ff569487)サポート Microsoft Direct3D 機能レベル 9 と[ **ResolveSharedResourceDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff569488)Direct3D 機能レベル 10 と 11 をサポートします。

Windows 8.1 以降、ユーザー モード ドライバーは独立した GPU と統合された GPU の間で共有されるクロス アダプターのリソースをサポートできます。 参照してください[ハイブリッド システムでクロス アダプターのリソースを使用して](using-cross-adapter-resources-in-a-hybrid-system.md)します。

 

 





