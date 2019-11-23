---
title: GPU からの情報のクエリ
description: GPU からの情報のクエリ
ms.assetid: 0d3942c2-3ae8-4eaa-9780-f146dd49699c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 705262fcc7ddeda70ce8f9bb8df750d02ea6cc21
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826003"
---
# <a name="querying-for-information-from-the-gpu"></a>GPU からの情報のクエリ


Direct3D ランタイムでは、出力のレンダーターゲットまたは出力頂点バッファー以外の GPU (graphics processing unit) の情報が必要になる場合があります。 GPU は CPU と並行して実行されるため、ユーザーモードのディスプレイドライバーは、GPU との非同期通信の性質を効率的に公開する関数を提供する必要があります。

Query オブジェクトは、ランタイムとドライバーが非同期通知に使用するリソースです。 クエリオブジェクトを作成するために、ランタイムはまずドライバーの[**CalcPrivateQuerySize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatequerysize)関数を呼び出します。これにより、ドライバーがクエリオブジェクトに必要なメモリ領域のサイズを指定できるようになります。 次に、ランタイムはドライバーの[**createquery (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createquery)関数を呼び出して、query オブジェクトを作成します。 *CalcPrivateQuerySize*と*CREATEQUERY (D3D10)* の呼び出しでは、ランタイムは、 *Pcreatequery*パラメーターが指す[**D3D10DDIARG\_Createquery**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createquery)構造体の**クエリ**メンバーの[**D3D10DDI\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10ddi_query)列挙体からクエリ型の値を提供します。

各クエリオブジェクトインスタンスは、*ビルド*、*発行*、および*通知*の3つの状態のいずれかに存在します。 ランタイムは、ドライバーの[**Querybegin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querybegin)関数を呼び出して、クエリオブジェクトをビルド状態に遷移させることができます。

**注**   すべての種類のクエリで*querybegin*がサポートされています。ただし、D3D10DDI\_QUERY\_EVENT と D3D10DDI\_query\_TIMESTAMP です。 D3D10DDI\_QUERY\_EVENT および D3D10DDI\_QUERY\_TIMESTAMP の構築概念は存在しません。

 

ランタイムは、ドライバーの[**Queryend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_queryend)関数を呼び出して、query オブジェクトを発行済み状態に遷移させることができます。 シグナル状態への遷移は、後でしばらく非同期に行われます。 ランタイムは、ドライバーの[**Querygetdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_querygetdata)関数を呼び出して、クエリがシグナル状態に遷移したかどうかを検出します。 クエリがシグナル状態の場合、 *Querygetdata*は、 *pData*パラメーターが指すメモリ領域内のクエリに適用されるデータを返すことができます。

同じ種類のすべてのクエリオブジェクトは、FIFO (先入れ先出し) です。 たとえば、D3D10DDI\_型のすべての query オブジェクトは、発行された順序に基づいて、FIFO の順序で\_イベントを完了します。 ただし、異なる種類のクエリオブジェクトは、重複した順序で完了または通知を行うことができます。 たとえば、D3D10DDI\_QUERY\_イベント型のクエリを実行する前に、ランタイムが D3D10DDI\_QUERY\_オク query を発行した後に D3D10DDI\_QUERY\_イベントクエリを発行した場合でも、クエリ\_オクルー型\_のクエリの前に完了できます。

ランタイムが query オブジェクトを必要としなくなった場合、ランタイムは、そのオブジェクトに対して以前に割り当てられたメモリ領域を解放し、ドライバーの[**Destroyquery (D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyquery)関数を呼び出して、ドライバーがこのメモリ領域にアクセスできなくなったことをドライバーに通知します。

 

 





