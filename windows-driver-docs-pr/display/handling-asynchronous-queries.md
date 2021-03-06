---
title: 非同期クエリの処理
description: 非同期クエリの処理
ms.assetid: b5e289db-eb9f-46e6-b221-4aa6661a9ce1
keywords:
- 非同期クエリ操作 WDK DirectX 9.0
- WDK の DirectX 9.0、非同期のクエリ操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28568aa2372049a7f01a772e5459292fe25cca47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372952"
---
# <a name="handling-asynchronous-queries"></a>非同期クエリの処理


## <span id="ddk_handling_asynchronous_queries_gg"></span><span id="DDK_HANDLING_ASYNCHRONOUS_QUERIES_GG"></span>


ドライバーで受信した非同期クエリ操作の処理、[コマンド ストリーム](command-stream.md)の[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)次の順序で説明したように関数:

1.  D3DDP2OP を受信した後、ドライバーはクエリのリソースを作成します\_と共に CREATEQUERY オペレーション コード、 [ **D3DHAL\_DP2CREATEQUERY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2createquery)コマンドの構造。ストリーム。

2.  ドライバーが、D3DDP2OP を受信した後、クエリの処理を開始\_と共に ISSUEQUERY オペレーション コード、 [ **D3DHAL\_DP2ISSUEQUERY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2issuequery)コマンド ストリーム内で構造体。

3.  場合は、D3DDP2OP を使用してクエリを送信した\_ISSUEQUERY 操作が完了しました、ドライバーが応答バッファーのサイズを設定する、 **dwErrorOffset**のメンバー、 [ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)構造と設定、 **ddrval** D3DHAL のメンバー\_D3D に DRAWPRIMITIVES2DATA\_[ok] を正常に完了します。 ドライバーには、受信コマンド バッファーが上書きされます[コマンド ストリーム](command-stream.md)送信ストリームに応答バッファーにします。 ドライバーのセット、 [ **D3DHAL\_DP2RESPONSE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2response)構造体の**bCommand** D3DDP2OP メンバー\_RESPONSEQUERY を示すためにその応答以前に発行するには、クエリが応答バッファーで利用できます。 各[ **D3DHAL\_DP2RESPONSEQUERY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2responsequery)応答バッファーの後に次のクエリに関連するデータ。

    -   D3DQUERYTYPE の BOOL\_イベント。 D3DDP2OP で応答する前に\_イベント RESPONSEQUERY、ドライバーの必要があります確実に、グラフィックス プロセッシング ユニット (GPU) がすべての処理を終了した[ **D3DHAL\_DP2OPERATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation)イベントに関連する操作。 つまり、のみ、ドライバーが問題のイベントの後に応答\_終了状態に発生します。 ドライバーでは、イベントをシグナル状態に設定する前に (設定**TRUE**)、GPU にピクセルが完成したラスタライズ、blt が完了するには、リソースが使用されていないと、フラッシュを実行する必要があります。 ドライバーに、イベントのブール値を設定する必要があります常に**TRUE**の応答時にします。
    -   D3DQUERYTYPE の DWORD\_遮蔽されます。 ドライバーは、ピクセルを z 検定のすべてのプリミティブの間で受け渡し、begin 行と、クエリの最後の数をこの dword 値を設定します。 マルチ サンプリングされた深度バッファーの場合、ドライバーはサンプルの数からピクセルの数を決定します。 ただし、表示デバイスあたりマルチ サンプリング z 検定の精度の場合、ピクセルの数に変換する必要があります一般に切り上げられます。 アプリケーションに対して「完全遮蔽されます」を効果的に意味する場合は 0、オクルー ジョン結果をチェックし、 マルチ サンプリングされた数量をピクセル数に変換するドライバーは、レンダー ターゲットのマルチ サンプリング変更を検出およびクエリの結果を適切に計算を続行する必要があります。
    -   [**D3DDEVINFO\_VCACHE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ns-d3d9types-_d3ddevinfo_vcache) D3DQUERYTYPE 構造\_VCACHE します。

    指定されたコマンド バッファーが小さすぎるため、すべての応答を書き込むドライバーの場合は、ドライバーにも送信 D3DDP2OP\_RESPONSECONTINUE 送信ストリームにします。

4.  ランタイムが判断した場合、ドライバーの[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数が成功した (**ddrval** D3DHAL のメンバー\_DRAWPRIMITIVES2DATA が D3D に設定\_[Ok])、ランタイム チェック、 **dwErrorOffset** D3DHAL のメンバー\_DRAWPRIMITIVES2DATA 応答が、ドライバーから使用できるかどうかを判断します。 これは、 **dwErrorOffset** 。 それ以外の応答がない場合、メンバーがゼロ**dwErrorOffset**応答バッファーのバイト単位のサイズです。 成功時にそのため、 *D3dDrawPrimitives2* (**ddrval** D3D に設定\_ok をクリック)、ドライバーを確認する必要がありますセットのみ**dwErrorOffset**に 0 以外の場合応答を利用できます。

5.  ランタイムは、返される応答バッファーを解析し、その内部データ構造体を更新します。

6.  ドライバーに送信される D3DDP2OP 場合\_RESPONSECONTINUE、ランタイムは、受信する空のコマンド バッファーを送信する[コマンド ストリーム](command-stream.md)ドライバーが複数の応答の記述を続行できるようにします。 ドライバーは、空のコマンド バッファーを処理できることを確認する必要があります。

 

 





