---
title: Direct3D DDI
description: Direct3D DDI
ms.assetid: 5b6f7c06-7f54-4fc4-9b94-5fb425b5b3c8
keywords:
- Direct3D WDK Windows 2000 ディスプレイ
- Direct3d WDK Windows 2000 ディスプレイ、Direct3D について
- グラフィックス WDK Windows 2000 ディスプレイ
- DDI WDK Direct3D
- ヘッダーファイル WDK Direct3D
- Direct3D WDK Windows 2000 display、ヘッダーファイル
- ディスプレイドライバーモデル WDK Windows 2000、Direct3D
- Windows 2000 display driver model WDK、Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11d648e3675069af17fb7ba63c6b9a4a3c1b1437
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839001"
---
# <a name="direct3d-ddi"></a>Direct3D DDI


## <span id="ddk_direct3d_gg"></span><span id="DDK_DIRECT3D_GG"></span>


Microsoft Direct3D device driver interface (DDI) は、ベンダーが Direct3D のハードウェアアクセラレータを提供できるようにするグラフィックスインターフェイスです。 インターフェイスは柔軟性があり、ベンダーはハードウェアの機能に応じて Direct3D アクセラレータを提供できます。 ドライバーライターは、ディスプレイドライバーの不可欠な部分として Direct3D DDI を実装します。

このセクションでは、Direct3D DDI について説明し、Direct3D driver writer の実装ガイドラインを示します。 リーダーは、Direct3D および Microsoft DirectDraw Api に精通していることと、DirectDraw DDI を含む Windows 2000 display driver モデルを把握していることを前提としています。

Windows 2000 以降のすべての Direct3D ドライバーは、Microsoft DirectX 7.0 以降の Direct3D ドライバーモデルに準拠している必要があります。 DirectX 8.0 ドライバーモデルは、Microsoft Windows XP でサポートされています。

Microsoft Windows 2000 以降用の Microsoft Direct3D ドライバーを作成するドライバーライターでは、次のヘッダーファイルを使用する必要があります。

<span id="D3DNTHAL.H"></span>*d3dnthal*  
ドライバーおよびドライバーレベルの構造体の定義によって実装されるコールバックのプロトタイプが含まれています。 [**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)列挙型は、このファイルで定義されています。 このヘッダーは*winddi*に含まれており、すべての Windows 2000 以降のディスプレイドライバーに含まれている必要があります。

<span id="D3DTYPES.H"></span>*d3dtypes*  
アプリケーションとドライバーの両方で使用される Direct3D 型定義が含まれています。 D3DHAL\_DP2OPERATION を除くすべての Direct3D 列挙型は、このヘッダーで定義されます。

<span id="D3DCAPS.H"></span>*d3dcaps*  
Direct3D ドライバーのさまざまな側面の機能を記述する構造体と定義が含まれています。

<span id="DX95TYPE.H"></span>*dx95type*  
ドライバー開発者は、Windows 2000 以降と Windows 98/Me の間で移植可能なドライバーコードを作成できます。

<span id="DDRAWINT.H"></span>*ddrawint*  
このヘッダーファイルは、ディスプレイドライバーの Microsoft DirectDraw 部分を開発するために winddi に含まれてい*ます。*

これらのヘッダーファイルはすべて、Windows Driver Kit (WDK) に付属しています。 以前のドライバー開発キット (DDKs) では、 *Perm3*ビデオ表示ディレクトリにある Direct3D ドライバー用のサンプルコードも提供しています。

Microsoft Windows Driver Kit (WDK) には、3Dlabs Permedia2 (*3Dlabs*) および 3Dlabs Permedia3 (*Perm3* ) サンプルの表示ドライバーが含まれていない  **ことに注意**してください。 これらのサンプルドライバーは、Windows Server 2003 SP1 DDK から入手できます。このドライバーは、WDHC web サイトの DDK-Windows Driver Development Kit ページからダウンロードできます。

 

Direct3d DDI の関数、構造体、および列挙体の参照ページは、「 [Direct3d Driver functions](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」、「 [direct3d driver 構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)体」、および「 [direct3d driver 列挙](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)体」にあります。

Direct3D インターフェイスの SDK 関連の側面の主なリファレンスは、Microsoft Windows SDK のドキュメントです。 *コンピューターグラフィックス:* Hughes によって発行された Feiner、van Dam、、およびによる原則とプラクティスは、一般的なグラフィックス参照です。

 

 





