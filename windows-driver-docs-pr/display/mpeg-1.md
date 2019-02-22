---
title: MPEG-1
description: MPEG-1
ms.assetid: be4db8ea-98fa-4693-a2ff-888499e97f38
keywords:
- Mpeg-1 WDK DirectX VA
- 旧バージョンと予測 WDK DirectX VA
- 双方向予測 WDK DirectX VA
- 予測は、WDK DirectX VA をブロックします。
- 旧バージョンと予測される予測 WDK DirectX VA をブロックします。
- 順方向予測予測 WDK DirectX VA をブロックします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1abfe22c8b8c7c34ef547b6d621ea7162d9459e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536138"
---
# <a name="mpeg-1"></a>MPEG-1


## <span id="ddk_mpeg_1_gg"></span><span id="DDK_MPEG_1_GG"></span>


Mpeg-1 ビデオ標準の ISO/IEC 11172 2 タイトルは。 この標準が H.261 後に開発し、そこから大幅に借用します。 Mpeg-1 標準では、ループのフィルターはありません。 代わりに、H.261 でサポートされている完全なサンプル精度よりも、フレーム間の移動の細かい精度を表す単純な半サンプル フィルターを使用します。

双方向と旧バージョンと予測は、2 つの追加の予測モードが追加されました。 これらの予測のモードでは、1 つの追加の参照をフレーム バッファーに格納する必要があります。 双方向予測のモードでは、順方向予測および予測の旧バージョンと予測のブロックを平均します。 前方と後方の予測のブロックの平均を計算の算術演算では、補間の予測を半分サンプリングされたブロックを作成するために似ています。 基本的な構造は、それ以外の場合、H.261 として同じです。

 

 





