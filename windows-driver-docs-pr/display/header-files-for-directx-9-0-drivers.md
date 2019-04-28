---
title: DirectX 9.0 ドライバー用のヘッダー ファイル
description: DirectX 9.0 ドライバー用のヘッダー ファイル
ms.assetid: b8628c92-0983-4f3a-af64-ef54201ee689
keywords:
- WDK DirectX 9.0 のヘッダー ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14cedd7365d61a9808853e33458d38baee90a57f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377959"
---
# <a name="header-files-for-directx-90-drivers"></a>DirectX 9.0 ドライバー用のヘッダー ファイル


## <span id="ddk_header_files_for_directx_9_0_drivers_gg"></span><span id="DDK_HEADER_FILES_FOR_DIRECTX_9_0_DRIVERS_GG"></span>


DirectX 9.0 ディスプレイ ドライバーのソース コードを含める必要があります、 *d3d9.h*ヘッダー ファイル。 ヘッダー ファイル*d3d9caps.h*と*d3d9types.h*に含まれる*d3d9.h*します。

DirectX 8.1 と以前のバージョンの DirectX のランタイムをサポートするドライバーのソース コード含める必要があります新旧両方の DirectX ヘッダーでは、たとえば*d3d.h*、 *d3d8.h*、および*d3d9.h*.

問題を避けるためには、DirectX 9.0 バージョンのドライバーを作成するときに、定義の DIRECT3D\_0x0900、ヘッダー ファイルをインクルードする前に、ドライバーのソース コードとバージョン。 これにより、DirectX 9.0 の機能」の説明に従って失われるの発生を防止、 [DIRECT3D\_バージョン](direct3d-version.md)トピック。 ビルド プロセスがヘッダー ファイル内のすべての必要なシンボルを取得するためには、含める*d3d9.h*と*d3d8.h*する前に*winddi.h*または*d3dnthal.h*.

 

 





