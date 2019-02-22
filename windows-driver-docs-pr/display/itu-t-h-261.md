---
title: ITU-T H.261
description: ITU-T H.261
ms.assetid: 00fb9001-2896-4ecd-b6ee-5b36bc6e72cd
keywords:
- ITU-T H.261 WDK DirectX VA
- H.261 WDK DirectX VA
- 予測は、WDK DirectX VA をブロックします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f66f4242a3db24e27de5fbfdc50de2dbfecad9d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537749"
---
# <a name="itu-t-h261"></a>ITU-T H.261


## <span id="ddk_itu_t_h_261_gg"></span><span id="DDK_ITU_T_H_261_GG"></span>


この標準の「px64 キロ ビット/秒、オーディオビジュアル サービスのビデオ コーデック」タイトルは ITU-T 推奨 H.261 します。 この推奨事項には、後で他のビデオ コーデック規格で使用される同じ基本的な設計が含まれています。 H.261 は 8 ビット サンプリングを使用して Y、Cb、Cr のコンポーネント、4:2:0 サンプリング、16 x 16 マクロ ブロック ベースの動き補正、8 x 8 IDCT、zigzag 逆係数、スカラーの量子化の組み合わせに基づいて係数の可変長のコーディングのスキャン実行の長さの値が 0 と量子化のインデックス値。

H.261 予測のすべてのブロックは、前の画像から順方向専用の予測を使用します。 H.261 では、正確な予測を半分サンプルのフィルターはありませんが、代わりに各マクロ ブロックの動き補正予測時にオンまたはオフにできますループ フィルター (H.261 仕様のセクション 3.2.3) と呼ばれる低域フィルターの種類を使用します。

**Annex D グラフィック**

ホストに戻すには、アクセラレータから 4 つのデコードされた画像を読み取り、そこに以上の解像度画像画像として表示するためのインターリーブ推奨 H.261 Annex D グラフィック転送モードをサポートできます。

 

 





