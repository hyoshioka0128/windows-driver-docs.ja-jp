---
title: DirectX 9.0 ドライバーの必須サポート
description: DirectX 9.0 ドライバーの必須サポート
ms.assetid: 9bc68101-c1be-470c-9eb7-9a689a2dd47c
keywords:
- 必要なドライバーサポート WDK DirectX 9.0
- DirectX 9.0 ドライバーサポート WDK
ms.date: 11/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f3be2fed7d33803a74f2156b6fd0957e69a6d3fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825888"
---
# <a name="required-directx-90-driver-support"></a>DirectX 9.0 ドライバーの必須サポート

DirectX 9.0 ランタイムは、ディスプレイドライバーが DirectX 7.0 以降のドライバーである場合、ハードウェアアクセラレータを提供します。 ただし、オペレーティングシステムによってバージョン9.0 ドライバーとしてドライバーが読み込まれるようにするには、次のセクションで説明されている機能を実装する必要があります。

- [2次元演算のサポート](supporting-two-dimensional-operations.md)

- [動的リソースのサポート](supporting-dynamic-resources.md)

- [サポート (頂点シェーダー宣言を)](supporting-vertex-shader-declarations.md)

- [ストリームオフセットのサポート](supporting-stream-offsets.md)

- [UBYTE4 Vertex 要素のレポートサポート](reporting-support-of-ubyte4-vertex-element.md)

- [レンダーターゲットを設定するためのコマンドのサポート](supporting-commands-for-setting-render-target.md)

- [シザー四角形の設定](setting-scissor-rectangle.md)

- [DirectX バージョンについて通知する](notifying-about-directx-version.md)

- [レポート DDI のバージョン](reporting-ddi-version.md)

DirectX 9.0 バージョンのドライバーは、以下をサポートする必要があります。

-   要求されたときに D3DCAPS9 構造体を返すことによって、デバイスの機能を報告します。 ドライバーは、D3DGDI2\_TYPE\_GETD3DCAPS9 value を使用して、D3DCAPS9 構造体を返します。**これは、** 「 [DirectX 8.0 スタイル Direct3D の報告」で説明されているように、D3DCAPS8 構造体を返す方法と似ています。機能](reporting-directx-8-0-style-direct3d-capabilities.md)。 この要求のサポートについては、「 [GetDriverInfo2](supporting-getdriverinfo2.md)のサポート」を参照してください。 D3DCAPS9 には、DirectX 9.0 と DirectX 8.0 に関連する機能の両方が含まれています。<br/><br/>DirectX 8.0 ランタイムによって照会された場合、ドライバーは D3DCAPS8 の DirectX 8.0 関連機能のみを報告する必要があります。

-   D3DFORMAT\_OP\_BUMPMAP フラグを設定すると、固定関数またはプログラミング可能なピクセルパイプのバンプマッピングをサポートするすべてのサーフェイス形式に対して、 [**Ddpixel 形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)構造体の**dwoperations**メンバーになります。

-   ドライバーがクエリの種類がサポートされていないことを示すだけで応答する場合でも、[非同期クエリ操作のレポートサポート](supporting-asynchronous-query-operations.md)。 詳細については、「[クエリの種類のサポートの検証](verifying-support-of-query-types.md)」を参照してください。<br/><br/>非同期クエリを実行すると、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI に新しい要件が2つ追加されます。 詳細については、「 [D3DDRAWPRIMITIVES2 DDI に要件を課す](imposing-requirements-on-the-d3ddrawprimitives2-ddi.md)」を参照してください。

-   アプリケーション[で、ビジー状態の存在キューを使用して他の処理を](processing-with-busy-present-queues.md)実行できるようにします。
