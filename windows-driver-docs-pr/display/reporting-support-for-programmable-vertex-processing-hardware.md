---
title: プログラミング可能な頂点シェーダー ハードウェアに対するサポートのレポート
description: プログラミング可能な頂点シェーダーのハードウェアのレポートをサポートする DirectX 8.0 レベル ドライバーの場合は、0 以外の場合、有効な頂点シェーダーのバージョン番号に D3DCAPS8 構造の VertexShaderVersion フィールドを設定があります。
ms.assetid: c77dae52-ed7c-4385-b085-df3e16e53c5e
keywords:
- 頂点シェーダー WDK DirectX 8.0 では、プログラミング可能なハードウェア
- プログラミング可能な頂点の WDK DirectX 8.0 のハードウェアの処理
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: fb39770b2db051e885ff52ba41be1b5149f45fd3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383243"
---
# <a name="reporting-support-for-programmable-vertex-shader-hardware"></a>プログラミング可能な頂点シェーダー ハードウェアに対するサポートのレポート

プログラミング可能な頂点シェーダーのハードウェアのレポートをサポートする DirectX 8.0 レベルのドライバーの設定があります、 **VertexShaderVersion** 0 以外の場合、有効な頂点シェーダーのバージョン番号に D3DCAPS8 構造体のフィールド。 **VertexShaderVersion** dword を最上位の単語には、値 0 xfffe が必要し、最下位のワードは実際のバージョン番号を格納します。 この単語の最下位バイトはマイナー バージョン番号を保持し、最上位バイトはメジャー バージョン番号を保持します。 この dword 値の形式は複雑なため、ドライバーの値を設定する必要があります**VertexShaderVersion** D3DVS マクロを使用して\_で定義されているバージョン*d3d8types.h*します。 たとえば、次のコード フラグメントをセット、 **VertexShaderVersion** 1.0 の機能レベルのサポートを示すためです。

```cpp
myD3DCaps8.VertexShaderVersion = D3DVS_VERSION(1, 0);
```

プログラミング可能な頂点シェーダーのサポートを報告しない場合は、次のコード フラグメントは使用されます。

```cpp
myD3DCaps8.VertexShaderVersion = D3DVS_VERSION(0, 0);
```

プログラミング可能な頂点の処理をサポートしていないドライバーを設定する必要があります**VertexShaderVersion**をゼロにします。

頂点シェーダーのバージョンを設定するだけでなく、ドライバーは、頂点の網かけが定数のレジスタの数を報告する必要があります。 1.0 頂点の網掛けの仕様をサポートするために、デバイスは、少なくとも 96 定数レジスタをいる必要があります。 ドライバーの定数レジスタの数を報告する、 **MaxVertexShaderConst** D3DCAPS8 構造体のフィールド。 たとえば、次のコード フラグメントは、必要なバージョン 1.0 の頂点シェーダー定数レジスタの最小数を報告します。

```cpp
myD3DCaps8.MaxVertexShaderConst = 96;
```

*d3d8types.h*定数レジスタが必要な頂点シェーダーの仕様のバージョン 1.0 の最小数のシンボルを定義します。 このシンボルは D3DVS\_CONSTREG\_最大\_V1\_0 とのドライバーは、96 を超える定数レジスタがサポートしている場合を除き、このシンボルを使用が推奨されます。

 

 





