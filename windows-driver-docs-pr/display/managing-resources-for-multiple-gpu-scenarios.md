---
title: 複数の GPU シナリオに対するリソースの管理
description: 複数の GPU シナリオに対するリソースの管理
ms.assetid: f3dc10b1-76e9-4f31-b253-149b6300611d
keywords:
- GPU WDK Windows 7 ディスプレイ
- GPU WDK Windows 7 display、multiple
- GPU WDK Windows 7 の表示、複数のリソースの管理
- 複数の Gpu WDK Windows 7 ディスプレイ
- 複数の Gpu WDK Windows 7 ディスプレイ、リソースの管理
- GPU WDK Windows 2008 Resource R2 ディスプレイ
- GPU WDK Windows 2008 Resource R2 display、multiple
- GPU WDK Windows 2008 Resource R2 の表示、複数のリソース管理
- 複数の Gpu WDK Windows 2008 Resource R2 ディスプレイ
- 複数の Gpu WDK Windows 2008 Resource R2 の表示、リソースの管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0943ba0f8e9e725fe0124389e56bd88e155550a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840579"
---
# <a name="managing-resources-for-multiple-gpu-scenarios"></a>複数の GPU シナリオに対するリソースの管理


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

複数の GPU シナリオのリソースを適切に管理するために、ユーザーモードの表示ドライバーは、Windows 7 に付属する新しいデバイスドライバーインターフェイス (DDI) を実装できます。 各リソースは、複数の Gpu がにレンダリングされるように、メモリ全体に分割されることがあります。 ドライバーはこの新しい DDI を実装して、新しいリソース所有者にマージされたリソースが含まれるように、各リソースを再マージできます。 この DDI 実装では、ドライバーは、リソースを変更する可能性のある部分的に構築されたコマンドバッファーをフラッシュする必要があります。 この DDI は、 [direct3d バージョン 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)の拡張機能として、および[direct3d バージョン10の DXGI DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に提供されています。 ドライバーは、Microsoft Direct3D の機能レベル9と[**ResolveSharedResourceDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions)をサポートするために、 [**ResolveSharedResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_resolvesharedresource)を実装して、direct3d 機能レベル10および11をサポートできます。

Windows 8.1 以降では、ユーザーモードドライバーは、個別の GPU と統合 GPU 間で共有されるクロスアダプターリソースをサポートできます。 「[ハイブリッドシステムでのクロスアダプタリソースの使用」を](using-cross-adapter-resources-in-a-hybrid-system.md)参照してください。

 

 





