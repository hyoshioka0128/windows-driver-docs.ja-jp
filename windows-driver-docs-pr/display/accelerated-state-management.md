---
title: 高速化状態管理
description: 高速化状態管理
ms.assetid: 276d3cdb-34bf-49e8-aae5-94315746c5ff
keywords:
- 高速状態管理 WDK Direct3D
- WDK Direct3D の状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2107b9227b56fe29389241990e5ea69991b6c34
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839835"
---
# <a name="accelerated-state-management"></a>高速化状態管理


## <span id="ddk_accelerated_state_management_gg"></span><span id="DDK_ACCELERATED_STATE_MANAGEMENT_GG"></span>


加速化された状態管理は、1回の呼び出しで API と DDI の間で大きな状態の変化を通知するためのメカニズムです。 このスキームを使用すると、アプリケーションは、1つの整数で定義された状態ブロックとして、状態セット呼び出しのコレクションを定義できます。 この整数をレンダー状態として送信すると、1回の呼び出しですべての状態の変更が実行されます。

これにより、必要な**IDirect3DDevice7:: SetRenderState**メソッド呼び出しの数が減り、API のオーバーヘッドが軽減されます。また、状態に応じて、独自のハードウェア固有の形式に変更を "プリコンパイル" できるようにすることで、ドライバーの効率を向上させることができます。各状態変更を実行するのではなく、定義をブロックします。 **IDirect3DDevice7:: SetRenderState**の詳細については、Direct3D SDK のドキュメントを参照してください。

ほとんどのアプリケーションは、いくつかの状態でのみ表示されるため、きめ細かな状態遷移が非常に重要になることはほとんどありません。 より重要なのは、ドライバーが一般的なレンダリングシナリオを切り替えるときに交換できる状態のブロックを定義できることです。 これは、全体的な状態管理の中心となるポイントです。

状態セットトークンは、ドライバーの状態を記録するために使用されます。 ハンドルは、状態のコレクションを参照します。 [**D3DHAL\_DP2STATESET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2stateset)構造体は、実行する状態セット操作をドライバーに通知します。

D3DHAL\_DP2STATESET 構造体の**Dwoperation**メンバーが D3DHAL\_STATESETBEGIN に設定されている場合、ドライバーは**dwoperation**メンバーに含まれているハンドルの状態の記録を開始します。 ドライバーは、D3DHAL\_STATESETEND の**Dwoperation**を受け取ると、状態の記録を停止します。

**Dwoperation**メンバーが D3DHAL\_STATESETDELETE の場合は、 **dwoperation**ハンドルによって参照される状態セットを削除する必要があります。

**Dwoperation**メンバーが D3DHAL\_STATESETEXECUTE の場合、 **dwoperation**ハンドルによって参照される状態ブロックをデバイスに適用する必要があります。

**Dwoperation**メンバーが D3DHAL\_STATESETCAPTURE の場合、ドライバーの現在の状態を特定の方法でキャプチャし、状態ブロックで定義されている現在の状態のスナップショットを提供する必要があります。 つまり、状態ブロックに既に存在する状態のみがキャプチャされます。 したがって、ステートブロックはマスクの一種として機能し、定義されている状態のみを記録します。 たとえば、状態ブロックに D3DRENDERSTATE\_ZENABLE レンダリング状態がある場合、D3DRENDERSTATE\_ZENABLE の現在の状態がキャプチャされ、状態ブロックに格納されます。 状態ブロックに D3DRENDERSTATE\_ZENABLE がない場合、その状態はキャプチャされません。

状態のグループ化を使用して、さまざまなレンダリングシナリオで若干変更できる汎用状態ブロックを作成します。 これらの定義済みのグループ (DirectX SDK ドキュメントの D3DSTATEBLOCKTYPE に列挙されています) では、定期的なレンダリングのシナリオに合わせて、後で状態の変更によって変更できるジェネリック状態ブロックを定義します。 たとえば、ドライバーは、100の汎用の定義済み状態ブロックを作成し、それぞれを少し変更して、異なるレンダリングシナリオに対応する場合があります。 状態ブロックの型は、D3DHAL\_DP2STATESET 構造体の**sbType**メンバーに渡されます。

**SbType**メンバーは、D3DHAL\_STATESETBEGIN および D3DHAL\_statesetbegin に対してのみ有効で、次のいずれかの D3DSTATEBLOCKTYPE 列挙型を使用して定義済みの状態ブロック型を指定します。 NULL の場合は NULL\_、すべての状態の場合は**NULL** 、ピクセル状態の場合は D3DSBT\_ピクセル状態、D3DSBT\_vertexstate。

ドライバーは、レンダー状態拡張機能を実装していない限り、**sbType**メンバーを無視する必要があります。 ドライバーが拡張レンダリング状態を実装している場合 (つまり、Direct3D ランタイムが提供するもの以外の状態をレンダリングする場合) は、 **sbType**を使用して、使用されている定義済みのレンダー状態の種類を判断できます。 この情報から、状態ブロックを適切に追加して、拡張機能をサポートする方法を決定できます。

 

 





