---
title: ストレッチ ブリット操作のサポート
description: ストレッチ ブリット操作のサポート
ms.assetid: 1d279e56-41fd-4189-84d2-858e51db281d
keywords:
- blit 拡張操作 WDK DirectX 9.0
- blit 操作 WDK DirectX 9.0 を拡張します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4269f3d0ed6899c4af7149c1f949c84692df79e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580884"
---
# <a name="supporting-stretch-blit-operations"></a>ストレッチ ブリット操作のサポート


## <span id="ddk_supporting_stretch_blit_operations_gg"></span><span id="DDK_SUPPORTING_STRETCH_BLIT_OPERATIONS_GG"></span>


ドライバーが伸縮ブリットを実行する方法は、それが実行されているプラットフォームに依存します。 Windows 98/Me プラットフォームときに、ドライバーの[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)関数ブリット要求を受け取ると、ドライバーのクリッピング四角形領域からの stretch の係数を計算することができます、 **rOrigDest**と**rOrigSrc**のメンバー、 [ **DD\_BLTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550474)構造体であり、ブリットの実行時に計算を考慮操作です。

ドライバーで計算し、DDBLT ブリット要求を受信すると、拡張要素を記録する DirectX 9.0 と後で NT ベースのオペレーティング システムでは、\_拡張\_フラグと DDBLT\_拡張\_プレゼンテーション\_STRETCHFACTOR フラグのセット、 **dwFlags** DD のメンバー\_BLTDATA します。 ドライバーでクリッピングを行わないソースと変換先四角形領域の拡張の係数を計算する、 **rSrc**と**bltFX** DD のそれぞれのメンバー\_DDBLTでBLTDATA\_拡張\_プレゼンテーション\_STRETCHFACTOR セット。 ドライバーがで DDBLTFX 構造体の次のメンバーから変換先のクリッピング四角形の領域を取得する必要がありますに注意してください。 **bltFX**、内の情報を使用しないと、 **rDest**メンバー。

-   構造体、DDCOLORKEY の次のメンバーから、左と上の座標、 **ddckDestColorkey** DDBLTFX のメンバー。
    -   左の座標から、 **dwColorSpaceLowValue** DDCOLORKEY のメンバー。
    -   上端の座標、 **dwColorSpaceHighValue** DDCOLORKEY のメンバー。
-   構造体、DDCOLORKEY の次のメンバーから右下隅の座標、 **ddckSrcColorkey** DDBLTFX のメンバー。
    -   右側の座標から、 **dwColorSpaceLowValue** DDCOLORKEY のメンバー。
    -   下端の座標、 **dwColorSpaceHighValue** DDCOLORKEY のメンバー。

ドライバーが Dword ではなく、符号付き整数としてこれらの座標を解釈することに注意してください。 また、ドライバーが伸縮係数の計算とグラフィックス デバイスに拡張要素をプログラミングする前にこれらの座標を形成する四角形を検証する必要がありますに注意してください。 DDBLTFX と DDCOLORKEY する方法の詳細については、最新の DirectDraw SDK ドキュメントを参照してください。

ドライバーが、ブリット DDBLT でを受信すると\_拡張\_プレゼンテーション\_STRETCHFACTOR のセットは、実際の中に、ドライバーはクリッピング四角形領域を使用する必要がありますされません。

ドライバーが、その後、DDBLT ブリット要求を受信すると\_プレゼンテーションと DDBLT\_最後\_フラグを設定したプレゼンテーション、ブリット操作でこの記録された拡張要素で、ドライバーを組み込むことができます。 完了すると、ドライバー、DDBLT で最終的なブリット\_最後\_プレゼンテーションのフラグを設定、ドライバーは、後続のブリット干渉を防ぐために stretch 係数レコードをクリアする必要があります。 DDBLT の詳細については\_プレゼンテーションと DDBLT\_最後\_プレゼンテーションのフラグを参照してください[プレゼンテーション](presentation.md)します。

拡張要素は、浮動小数点演算であるため、すべてのグラフィックス デバイスをサポートできます。 そのため、このようなデバイスのドライバーでは、計算して、拡張要素を使用する必要はありません。 ただし、stretch 係数の計算はサポートされていない場合でも、DirectX 9.0 と以降のバージョンのドライバー、NT ベースのオペレーティング システムにする必要がありますもの存在を確認、DDBLT\_拡張\_プレゼンテーション\_STRETCHFACTOR フラグ実際の blit 操作を実行しようとしているため、DDBLT\_拡張\_プレゼンテーション\_STRETCHFACTOR フラグが設定されてレンダリングの破損が発生するとします。

拡張 blit フラグの詳細については、次を参照してください。[拡張 Blt フラグ](extended-blt-flags.md)します。

 

 





