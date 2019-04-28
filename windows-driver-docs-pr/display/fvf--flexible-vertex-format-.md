---
title: FVF (柔軟な頂点形式)
description: FVF (柔軟な頂点形式)
ms.assetid: 206f4275-bcb8-4e8e-9c11-c6fb5d9c561d
keywords:
- 頂点形式 WDK Direct3D
- 柔軟な頂点形式 WDK Direct3D
- FVF WDK Direct3D
- Direct3D WDK Windows 2000 の表示、柔軟な頂点の書式設定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c94d4dda73a0bbb950ac4ce96257c4595fbc575
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377990"
---
# <a name="fvf-flexible-vertex-format"></a>FVF (柔軟な頂点形式)


## <span id="ddk_fvf_gg"></span><span id="DDK_FVF_GG"></span>


ドライバーの[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)コールバックは、柔軟な頂点の形式 (FVF) で頂点データを受信します。 頂点の形式は、柔軟であるために、このデータに対して定義された包括的なデータ構造はありません。 ドライバーは、FVF のすべての機能を実装する必要があります。

Microsoft DirectX 7.0 を含む 1 D、3 D、および通常の 2D テクスチャだけでなく 4 D テクスチャ FVF 更新プログラムがあります。 この更新プログラムの詳細については、次を参照してください。 [FVF 更新](fvf-update.md)します。 参照してください、 *Perm3*ドライバーとこれらのトピックの詳細については、DirectX SDK ドキュメントのサンプルです。

**注**   、Microsoft Windows Driver Kit (WDK) に 3 dlabs Permedia3 サンプルのディスプレイ ドライバーが含まれていません (*Perm3.h*)。 Windows Server 2003 SP1 ドライバー開発キット (DDK)、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロードできるこのサンプル ドライバーを取得できます。

 

 

 





