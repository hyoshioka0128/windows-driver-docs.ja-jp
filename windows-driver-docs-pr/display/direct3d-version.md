---
title: DIRECT3D_VERSION
description: DIRECT3D_VERSION
ms.assetid: 09032f06-d31f-4d9f-80bd-e6b9b8d5cbaa
keywords:
- DirectX 8.0 リリース ノートには Windows 2000 の WDK の表示、ヘッダー ファイル
- WDK DirectX 8.0 のヘッダー ファイル
- DIRECT3D_VERSION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6f1944cb05f34c0b2618caf17d5b630b2bf59d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357962"
---
# <a name="direct3dversion"></a>DIRECT3D\_バージョン


## <span id="ddk_direct3d_version_gg"></span><span id="DDK_DIRECT3D_VERSION_GG"></span>


DirectX のディスプレイ ドライバーには、DirectX 7.0 と以前のバージョンの DirectX のランタイムをサポートする必要があります。 たとえば新旧両方の DirectX ヘッダーを含める必要は*d3d.h*と*d3d8.h*します。 ただし、DIRECT3D のプリプロセッサ シンボルの定義に問題が生じる\_バージョン。 このプリプロセッサのシンボルは、どの構造体と関数が含まれるをするヘッダー ファイルで使用されます。 場合は、DIRECT3D\_バージョンは既に定義されていません、DirectX のヘッダー ファイルは、DIRECT3D の値を設定\_バージョン用に設計された、最新バージョンにします。 したがって、 *d3d.h* DIRECT3D を設定\_は 0x0700 するバージョンと*d3d8.h* DIRECT3D を設定\_0x0800 するバージョン。 場合*d3d.h*する前に、ソースに含まれる*d3d8.h*、Direct3D 8.0 の新機能が定義されていないと、コンパイラ エラーが発生します。

これを回避するには、DIRECT3D を定義\_ヘッダー ファイルをインクルードする前に 0x0800 するバージョン。 ヘッダー ファイルに必要なすべてのシンボルを取得するために含める前に d3d8.h *winddi.h*または*d3dnthal.h*します。

 

 





