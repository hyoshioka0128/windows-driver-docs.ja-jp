---
title: GPU からの情報のクエリ
description: GPU からの情報のクエリ
ms.assetid: 0d3942c2-3ae8-4eaa-9780-f146dd49699c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 151c8d497be218e5691c91e2529968eed611b46d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385047"
---
# <a name="querying-for-information-from-the-gpu"></a>GPU からの情報のクエリ


出力ターゲットまたは出力の頂点バッファーを表示する以外、Direct3D のランタイムは、グラフィックス処理装置 (GPU) からの情報を必要があります。 GPU は、CPU と並列で実行するため、ユーザー モードのディスプレイ ドライバーは、GPU との通信の非同期の性質を効率的に公開する関数を指定します。

クエリ オブジェクトは、非同期通知のランタイムとドライバーを使用するリソースです。 クエリ オブジェクトを作成するランタイム最初は、ドライバーの[ **CalcPrivateQuerySize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatequerysize)関数が、ドライバーは、ドライバーはクエリ オブジェクトを必要とするメモリ領域のサイズを提供できるようにします。 ランタイムを呼び出してドライバーの[ **CreateQuery(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createquery)クエリ オブジェクトを作成する関数。 *CalcPrivateQuerySize*と*CreateQuery(D3D10)* 呼び出し、クエリ型の値を提供する、ランタイム、 [ **D3D10DDI\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)で列挙、**クエリ**のメンバー、 [ **D3D10DDIARG\_CREATEQUERY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createquery)構造体、 *pCreateQuery*パラメーターをポイントします。

各クエリ オブジェクト インスタンスが 3 つの状態のいずれかに存在します:*構築*、*発行*と*シグナル*。 ランタイムが呼び出す、ドライバーの[ **QueryBegin** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querybegin)クエリ オブジェクトをビルド状態を遷移する関数。

**注**  すべてのクエリの型のサポート*QueryBegin* D3D10DDI を除く\_クエリ\_イベントと D3D10DDI\_クエリ\_タイムスタンプ。 D3D10DDI 用構成の概念がない\_クエリ\_イベントと D3D10DDI\_クエリ\_タイムスタンプ。

 

ランタイムが呼び出す、ドライバーの[ **QueryEnd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_queryend)発行済みの状態をクエリ オブジェクトを移行する関数。 シグナル状態に遷移を後で非同期に実行します。 ランタイムが呼び出す、ドライバーの[ **QueryGetData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata)クエリがシグナル状態に遷移するかどうかを検出する関数。 クエリがシグナルの状態の場合*QueryGetData*メモリ領域で、クエリに適用されるデータを渡すことができますが、 *pData*パラメーターが指します。

同じ種類のすべてのクエリ オブジェクトは、FIFO (つまり、先入れ先出しです)。 たとえば、すべてのクエリの D3D10DDI 型のオブジェクト\_クエリ\_発行済みの順序に基づいて、FIFO の順序で完了イベント。 ただし、さまざまな種類のクエリ オブジェクトは、完了または重複する順番を通知します。 D3D10DDI の種類のクエリ例:\_クエリ\_D3D10DDI の種類のクエリの前に完了できるイベント\_クエリ\_オクルー ジョン、ランタイム、D3D10DDI を発行する場合でも\_クエリ\_イベントランタイムは、D3D10DDI を発行した後にクエリ\_クエリ\_オクルー ジョン クエリ。

ランタイムが、ランタイムが以前、オブジェクトに割り当てられたし、ドライバーを呼び出すことは、メモリ領域を解放する、ランタイムでは、クエリ オブジェクトが必要なくなる、 [ **DestroyQuery(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyquery)関数ドライバーでこのメモリ領域を不要になったアクセスできることをドライバーに通知します。

 

 





