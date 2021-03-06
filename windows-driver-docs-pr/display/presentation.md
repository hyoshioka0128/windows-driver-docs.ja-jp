---
title: 効果
description: 効果
ms.assetid: 23a01b5b-0654-4c43-ac96-a75810fa20df
keywords:
- Windows 2000 の WDK の表示、プレゼンテーションの DirectX 8.0 リリース ノートします。
- WDK DirectX 8.0 のプレゼンテーション
- レンダリング結果表示の WDK DirectX 8.0
- 表示される結果 WDK DirectX 8.0
- DDLT_PRESENTATION
- DDBLT_LAST_PRESENTATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 563fabb561e7ee9f1048f7c6044542446f32a53d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369282"
---
# <a name="presentation"></a>効果


## <span id="ddk_presentation_gg"></span><span id="DDK_PRESENTATION_GG"></span>


DirectX 8.0「プレゼンテーション」(または、ユーザーに表示されるレンダリングの結果を行う) の概念を形式化する api。 以前は、全画面表示モードで反転ページまたはウィンドウ モードでの中のいずれか、これが実現されました。 アプリケーションを使用して、新しい**存在**full を実行する API フリッピングまたはウィンドウ表示モード中の画面します。 ただし、このメカニズムはまだ公開されていません、DDI レベル。 ランタイムは単にマップ、**存在**するか、API、 [ *DdFlip* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)または[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) DDI エントリアプリケーション モードによってポイント。

DirectX の 8.0 が blt 操作が実際にときの通知としてドライバーに渡される 2 つの新しい DirectDraw blt フラグを追加の一部を**存在**し、そのため、フレームの境界線をマークします。 これらの新しいフラグは DDBLT\_プレゼンテーションと DDBLT\_最後\_プレゼンテーション。 1 つのクリッピングがありますので、2 つのフラグが必要な**存在**ドライバーでの複数の blt 操作の呼び出しを呼び出します。 この場合は、すべての結果として呼び出される blt の**存在**操作がある、DDBLT\_プレゼンテーション フラグを設定します。 ただし、シーケンスの最終的な blt のみを使用して実行する、**存在**、DDBLT が\_最後\_プレゼンテーション ビットが設定されます。 そのため、blt を実装するために使用する場合、**存在**呼び出し、ドライバーが、DDBLT と 0 個以上の blt\_プレゼンテーション ビットが設定後に、両方の DDLT で 1 つだけ blt\_プレゼンテーションと DDBLT\_最後\_プレゼンテーション ビットを設定します。 これらのフラグは、アプリケーションで設定しないでください。 これらのフラグ、blt を渡して、ランタイムのみが許可されます。 さらに、これらのフラグでは、DirectX 8.0 DDI をサポートしているドライバーに渡されるだけです。

ドライバーは、最大 3 つのフレームをキューにのみ許可されます。 ドライバーで DDBLT blt 呼び出しを認識する場合\_DDBLT の 3 つが既にプレゼンテーション セットとその\_最後\_プレゼンテーション blt でキューに DDERR の呼び出しが失敗する必要があります\_WASSTILLDRAWING します。 キューのドレインが十分になるまで、ランタイムが再試行されます。

ドライバーは、ときに、DDBLT に効果的を判断できない場合\_最後\_プレゼンテーション blt キューでは廃止されましたし、すべてのドライバーにフレームをいないキューが必要があります。 DDBLT\_最後\_DDERR を返すには、このようなドライバーが発生する必要がありますプレゼンテーション\_WASSTILLDRAWING アクセラレータが、アプリケーションを呼び出した場合と同様、完全に終了するまで**ロック**で、呼び出しの前にソース画面**Blt**します。

最後に、ウィンドウ、複数のアプリケーションに同時に実行されている場合、ドライバーは、プライマリではなく、各 blt のソースに基づいたプレゼンテーション blt をカウントする必要があります、3 つのフレーム ウィンドウ/レンダー ターゲットごとのキューに入れ、ドライバーが許可されている、します。 これは、結果、パフォーマンスが向上します。

 

 





