---
title: 高速化状態管理
description: 高速化状態管理
ms.assetid: 276d3cdb-34bf-49e8-aae5-94315746c5ff
keywords:
- WDK Direct3D の高速化された状態管理
- WDK Direct3D を状態します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60bbd56a4f0ba43041f95a4e0dc1508ba3ab2756
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323803"
---
# <a name="accelerated-state-management"></a>高速化状態管理


## <span id="ddk_accelerated_state_management_gg"></span><span id="DDK_ACCELERATED_STATE_MANAGEMENT_GG"></span>


高速化された状態の管理は、API および DDI 間で大規模な状態の変更を 1 回の呼び出しで通信するためのメカニズムです。 このスキームにより、1 つの整数によって定義された状態のブロックとして状態設定呼び出しのコレクションを定義するアプリケーションです。 レンダリング状態としてこの整数値を送信することは、1 回の呼び出しですべての状態変更を実行します。

数を減らすことで、API がオーバーヘッド削減**IDirect3DDevice7::SetRenderState**メソッドの呼び出しは必要に応じて、および「プリコンパイル」段階の変更、独自にすることにより、ドライバーの効率を向上できます状態ブロック時にハードウェアに固有の書式を定義するのではなく各状態の変化の実行で。 **IDirect3DDevice7::SetRenderState** Direct3D SDK ドキュメントの説明は、

ほとんどのアプリケーションは、詳細な状態遷移のことが重要めったにありませんごく少数の状態で表示します。 さらに重要な新機能は、レンダリングの一般的なシナリオ間 driver スイッチと入れ替えることが状態のブロックを定義できることです。 これは、全体の高速化された状態の管理ポイントです。

状態セット トークンを使用して、ドライバーの状態を記録します。 ハンドルは、状態のコレクションを表します。 [ **D3DHAL\_DP2STATESET** ](https://msdn.microsoft.com/library/windows/hardware/ff545844)構造体を実行するには、どのような状態セット操作に関するドライバーに通知します。

場合、 **dwOperation** 、D3DHAL のメンバー\_DP2STATESET 構造が D3DHAL に設定されている\_に含まれているハンドルの状態の記録が開始 STATESETBEGIN、ドライバー、**について**メンバー。 ドライバーが受信すると、 **dwOperation** D3DHAL の\_STATESETEND、状態の記録を停止します。

場合、 **dwOperation**メンバーが D3DHAL\_STATESETDELETE、状態のセットで参照される、**について**ハンドルを削除する必要があります。

場合、 **dwOperation**メンバーが D3DHAL\_STATESETEXECUTE、によって参照される状態のブロック、**について**ハンドルはデバイスに適用する必要があります。

場合、 **dwOperation**メンバーが D3DHAL\_STATESETCAPTURE、ドライバーでは、現在の状態をキャプチャするか、特定の方法で状態ブロックで定義されている現在の状態のスナップショットを提供します。 つまり、既に状態ブロックされている状態のみがキャプチャされます。 したがって、状態のブロックは、マスク、のみが定義されている状態の記録の一種として機能します。 例では、D3DRENDERSTATE がある場合、\_ZENABLE D3DRENDERSTATE の状態のブロックでの状態、現在の状態を表示\_ZENABLE がキャプチャされ、状態のブロックを入力します。 D3DRENDERSTATE がない場合は\_ZENABLE の状態をブロックし、その状態はキャプチャされません。

状態のグループは、さまざまなレンダリングのシナリオを若干変更可能な汎用状態ブロックの作成に使用されます。 (D3DSTATEBLOCKTYPE で列挙、DirectX SDK のドキュメントで) これらの定義済みグループでは、予想される定期的なレンダリングのシナリオに対応する状態の変更を後で変更可能な汎用的な状態のブロックを定義します。 など、ドライバーは、100 のジェネリックの定義済みの状態のブロックを作成し、それぞれ別のレンダリング シナリオに対応するために少しを変更する可能性があります。 状態ブロックの型が渡された、 **sbType** 、D3DHAL のメンバー\_DP2STATESET 構造体。

**SbType**メンバーに対してのみ有効です D3DHAL\_STATESETBEGIN と D3DHAL\_STATESETEND し次 D3DSTATEBLOCKTYPE 列挙型のいずれかの定義済みの状態のブロックの型を指定します。**NULL**のない状態では、D3DSBT\_D3DSBT、すべての状態のすべて\_、ピクセルの状態や D3DSBT PIXELSTATE\_VERTEXSTATE の頂点の状態。

ドライバーを無視する必要があります、**sbType**メンバーを実装しない限り、表示拡張機能の状態。 Direct3D のランタイムを提供するもの以外の状態をレンダリングは、拡張ドライバーの実装では、状態をレンダリングする場合は、使用できる**sbType**の種類を決定する定義済みの描画状態が使用されています。 この情報から、その拡張機能をサポートするために、状態のブロックを適切に追加する方法を判断ができます。

 

 





