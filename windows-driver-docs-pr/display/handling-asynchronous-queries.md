---
title: 非同期クエリの処理
description: 非同期クエリの処理
ms.assetid: b5e289db-eb9f-46e6-b221-4aa6661a9ce1
keywords:
- 非同期クエリ操作 WDK DirectX 9.0
- クエリ操作 WDK DirectX 9.0、非同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ded9cb09e581d8b634d4a8ad08e4539eb4f135c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838911"
---
# <a name="handling-asynchronous-queries"></a>非同期クエリの処理


## <span id="ddk_handling_asynchronous_queries_gg"></span><span id="DDK_HANDLING_ASYNCHRONOUS_QUERIES_GG"></span>


ドライバーは、次の順序で説明されているように、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の[コマンドストリーム](command-stream.md)で受信した非同期クエリ操作を処理します。

1.  ドライバーは、コマンドストリームで[**D3DHAL\_DP2CREATEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2createquery)構造と共に D3DDP2OP\_createquery 操作コードを受け取ると、クエリのリソースを作成します。

2.  ドライバーは、コマンドストリームで[**D3DHAL\_DP2ISSUEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2issuequery)構造と共に D3DDP2OP\_ISSUEQUERY 操作コードを受け取ると、クエリの処理を開始します。

3.  前に D3DDP2OP\_ISSUEQUERY 操作を使用してクエリを送信した場合、ドライバーは[**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造体の**dwerroroffset**メンバーの応答バッファーのサイズを設定し、正常に完了するには、D3DHAL\_DRAWPRIMITIVES2DATA の ddrval メンバーが D3D\_OK です。 ドライバーは、受信[コマンドストリーム](command-stream.md)のコマンドバッファーを、送信ストリームの応答バッファーで上書きします。 ドライバーは、 [**D3DHAL\_DP2RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2response)構造体の**BCOMMAND**メンバーを D3DDP2OP\_responsequery に設定して、以前に発行されたクエリに対する応答を応答バッファーで利用できることを示します。 応答バッファー内の各[**D3DHAL\_DP2RESPONSEQUERY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2responsequery)の後に、クエリに関連する次のデータが続きます。

    -   D3DQUERYTYPE\_イベントのブール値。 イベントの D3DDP2OP\_RESPONSEQUERY に応答する前に、ドライバーは、イベントに関連付けられているすべての[**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)操作の処理がグラフィックス処理ユニット (GPU) によって完了されていることを確認する必要があります。 つまり、ドライバーは、イベントの問題\_終了状態が発生した後にのみ応答します。 ドライバーによってイベントがシグナル状態 ( **TRUE**に設定) に設定される前に、GPU がフラッシュを実行して、ピクセルのラスタライズ、blts の完了、リソースの使用が終了していることを確認する必要がある場合があります。 応答する場合、ドライバーは常にイベントのブール値を**TRUE**に設定する必要があります。
    -   D3DQUERYTYPE\_オクルーの DWORD です。 ドライバーは、クエリの begin と end の間にあるすべてのプリミティブに対して z 検定が渡されたピクセル数にこの DWORD を設定します。 深度バッファーがマルチサンプリングテクスチャの場合、ドライバーはサンプル数からピクセル数を決定します。 ただし、ディスプレイデバイスがマルチサンプリングの z 検定精度を持つことができる場合は、通常、ピクセル数への変換が切り上げられます。 その後、アプリケーションは、オクルージョンの結果を0として確認し、事実上 "完全 occluded" を意味します。 マルチサンプリングテクスチャ数量をピクセル数に変換するドライバーは、レンダーターゲットのマルチサンプリング変更を検出し、クエリ結果を適切に計算し続ける必要があります。
    -   D3DQUERYTYPE\_VCACHE の[**D3DDEVINFO\_VCACHE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ns-d3d9types-_d3ddevinfo_vcache)構造体。

    指定されたコマンドバッファーが小さすぎて、すべての応答を書き込むことができない場合、ドライバーは送信ストリームで D3DDP2OP\_応答を送信します。

4.  ランタイムによって、ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数が成功したと判断された場合 (D3DHAL\_DRAWPRIMITIVES2DATA の**DDRVAL**メンバーが D3D\_OK) に設定されている場合、ランタイムは D3DHAL の**dwerroroffset**メンバーを調べ\_DRAWPRIMITIVES2DATA を使用すると、ドライバーから応答を利用できるかどうかを判断できます。 応答がない場合、この**Dwerroroffset**メンバーは0です。それ以外の場合、 **Dwerroroffset**は、応答バッファーのサイズ (バイト単位) です。 したがって、 *D3dDrawPrimitives2* (**DDRVAL**が D3D\_OK) に成功した場合、応答が使用可能な場合、ドライバーは**dwerroroffset**を0以外に設定する必要があることを確認する必要があります。

5.  ランタイムは、返された応答バッファーを解析し、内部データ構造を更新します。

6.  ドライバーが D3DDP2OP\_応答を送信した場合、ランタイムは、ドライバーがより多くの応答を書き込むことができるように、受信[コマンドストリーム](command-stream.md)に空のコマンドバッファーを送信します。 ドライバーは、空のコマンドバッファーを処理できることを確認する必要があります。

 

 





