---
title: Direct3D DDI
description: Direct3D DDI
ms.assetid: 5b6f7c06-7f54-4fc4-9b94-5fb425b5b3c8
keywords:
- Direct3D WDK Windows 2000 の表示
- Direct3D について、Direct3D WDK Windows 2000 の表示
- グラフィックス WDK Windows 2000 を表示します。
- DDI WDK Direct3D
- WDK Direct3D のヘッダー ファイル
- Direct3D WDK Windows 2000 の表示、ヘッダー ファイル
- ドライバー モデル WDK Windows 2000 では、Direct3D を表示します。
- Windows 2000 ディスプレイ ドライバー モデル WDK、Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 992732431b885822997f7ac21afa063c1d036a08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357950"
---
# <a name="direct3d-ddi"></a>Direct3D DDI


## <span id="ddk_direct3d_gg"></span><span id="DDK_DIRECT3D_GG"></span>


マイクロソフトの Direct3D デバイス ドライバー インターフェイス (DDI) は、Direct3D ハードウェア アクセラレータを提供するベンダーを許可するグラフィックス インターフェイスです。 インターフェイスは柔軟性が高く、ベンダーがハードウェア機能に応じて、Direct3D の機能を提供することができます。 ドライバーの作成者は、ディスプレイ ドライバーの不可欠な部分として Direct3D DDI を実装します。

このセクションでは、Direct3D DDI、について説明し、Direct3D ドライバー ライターの実装に関するガイドラインを提供します。 リーダーが Direct3D と Microsoft DirectDraw Api について理解して、DirectDraw DDI を含む、Windows 2000 ディスプレイ ドライバー モデルを確実に理解があると見なされます。

Windows 2000 以降のすべての Direct3D ドライバーは、Microsoft DirectX 7.0 またはそれ以降の Direct3D ドライバー モデルに従う必要があります。 DirectX 8.0 ドライバー モデルは、Microsoft Windows XP でサポートされます。

Microsoft Windows 2000 以降、マイクロソフトの Direct3D ドライバーを作成しているドライバーの作成者は、次のヘッダー ファイルを使用してください。

<span id="D3DNTHAL.H"></span>*d3dnthal.h*  
ドライバー レベルの構造体のドライバーによって実装されるコールバックのプロトタイプと定義が含まれています。 [ **D3DHAL\_DP2OPERATION** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)列挙型は、このファイルで定義されます。 このヘッダーが含まれている*winddi.h*、すべての Windows 2000 に含める必要があるあり、ドライバーを後で表示します。

<span id="D3DTYPES.H"></span>*d3dtypes.h*  
アプリケーションとドライバーの両方で使用される、Direct3D 型定義が含まれています。 D3DHAL を除く\_DP2OPERATION、その他すべての Direct3D 列挙型は、このヘッダーで定義されます。

<span id="D3DCAPS.H"></span>*d3dcaps.h*  
構造体と Direct3D のドライバーのさまざまな側面の機能を記述する定義が含まれています。

<span id="DX95TYPE.H"></span>*dx95type.h*  
により、ポータブルの Windows 2000 以降と Windows 98 は、ドライバーのコードを記述するドライバー開発者/me.

<span id="DDRAWINT.H"></span>*ddrawint.h*  
このヘッダー ファイルに含まれている*winddi.h*、ディスプレイ ドライバーの Microsoft DirectDraw 部分を開発するが必要です。

これらのヘッダー ファイルのすべては、Windows Driver Kit (WDK) に付属しています。 前の Driver Development Kits (Ddk) は、Direct3D ドライバーのサンプル コードを提供することも、 *Perm3*ビデオ ディスプレイのディレクトリ。

**注**   3 dlabs permedia2 チップが、Microsoft Windows Driver Kit (WDK) に含まれていない (*3dlabs.htm*) と 3 dlabs Permedia3 (*Perm3.htm* ) ディスプレイ ドライバーのサンプルです。 これらのサンプル ドライバーは、DDK - WDHC web サイトの Windows ドライバー開発キットのページからダウンロードできる Windows Server 2003 SP1 DDK から取得できます。

 

Direct3D DDI 関数では、構造体、ページを参照し、列挙型が記載[Direct3D ドライバー関数](https://msdn.microsoft.com/library/windows/hardware/ff552853)、 [Direct3D ドライバー構造](https://msdn.microsoft.com/library/windows/hardware/ff552858)、および[Direct3D ドライバー列挙型](https://msdn.microsoft.com/library/windows/hardware/ff552850).

Direct3D インターフェイスの SDK に関連する側面のプライマリ参照では、Microsoft Windows SDK ドキュメントです。 *コンピューターのグラフィックス:基本原則と実習*Foley、van ダム、Feiner、および Hughes、addison-wesley 発行された、このによっては役に立つ一般的なグラフィックスの参照。

 

 





