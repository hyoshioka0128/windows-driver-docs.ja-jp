---
title: DirectX 9.0 ドライバーの必須サポート
description: DirectX 9.0 ドライバーの必須サポート
ms.assetid: 9bc68101-c1be-470c-9eb7-9a689a2dd47c
keywords:
- WDK DirectX 9.0 の必要なドライバーのサポート
- DirectX 9.0 ドライバー WDK のサポート
ms.date: 11/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: eeb8066d1e179b29f59581fc1670b4e3b721964e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376592"
---
# <a name="required-directx-90-driver-support"></a>DirectX 9.0 ドライバーの必須サポート

ディスプレイ ドライバーが、DirectX 7.0 またはそれ以降のドライバーの場合、DirectX 9.0 ランタイムはハードウェア アクセラレータを指定します。 ただし、バージョン 9.0 ドライバーとしてオペレーティング システムによって読み込まれるドライバーの場合は、以下のセクションで説明されている機能を実装にする必要があります。

- [2 次元の操作をサポートしています。](supporting-two-dimensional-operations.md)

- [動的リソースのサポート](supporting-dynamic-resources.md)

- [頂点シェーダーの宣言をサポートしています。](supporting-vertex-shader-declarations.md)

- [オフセット Stream のサポート](supporting-stream-offsets.md)

- [レポートの UBYTE4 頂点要素のサポート](reporting-support-of-ubyte4-vertex-element.md)

- [レンダー ターゲットの設定のコマンドをサポートしています。](supporting-commands-for-setting-render-target.md)

- [シザリング四角形の設定](setting-scissor-rectangle.md)

- [DirectX のバージョンについて通知します。](notifying-about-directx-version.md)

- [DDI バージョンのレポート](reporting-ddi-version.md)

DirectX 9.0 バージョンのドライバーをサポートする必要があります。

-   要求されたときに、D3DCAPS9 構造体を返すことによってそのデバイスの機能を報告します。 ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_D3DCAPS8 構造体を返します」の説明に従って方法と同様にGETD3DCAPS9値[DirectX 8.0 スタイル Direct3D の機能を reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 この要求のサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。 D3DCAPS9 には、DirectX 9.0 と DirectX 8.0 関連機能の両方が含まれています。<br/><br/>ドライバーは、DirectX 8.0 D3DCAPS8 DirectX 8.0 ランタイムから照会されたときの機能に関連する専用のレポートに続ける必要があります。

-   設定、D3DFORMAT\_OP\_BUMPMAP フラグ、 **dwOperations**のメンバー、 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)すべてサーフェスの形式の構造固定関数またはピクセル プログラミング可能なのか、パイプのバンプ マッピングをサポートすることができます。

-   Reporting[非同期クエリ操作のサポート](supporting-asynchronous-query-operations.md)場合でも、クエリの種類がサポートされていないことを示すことにより、ドライバーは応答のみです。 詳細については、次を参照してください。[クエリ型のサポートを確認する](verifying-support-of-query-types.md)します。<br/><br/>2 つの新しい要件を課す非同期的にクエリを実行する、 [ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI します。 詳細については、次を参照してください。 [D3dDrawPrimitives2 DDI の要件を課す](imposing-requirements-on-the-d3ddrawprimitives2-ddi.md)します。

-   アプリケーションの実行ができるように[処理でビジー状態の存在するキュー](processing-with-busy-present-queues.md)します。
