---
title: コマンド ストリーム
description: コマンド ストリーム
ms.assetid: 125e2072-42d6-4d4b-aec9-94b40a9d493c
keywords:
- Direct3D WDK Windows 2000 display、操作コード
- 操作コード WDK Direct3D
- コマンドストリーム WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc48b1d9a7be4776b964df9b76afa74bd59bd744
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839801"
---
# <a name="command-stream"></a>コマンド ストリーム


## <span id="ddk_command_stream_gg"></span><span id="DDK_COMMAND_STREAM_GG"></span>


ドライバーレベルでは、手順は[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)の呼び出しの形式になります。 入力構造[**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)には、コマンドバッファーへのポインターが含まれています。 これは、 [**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体のシーケンスです。 これらの各構造体には、バッファー内でそれに続くデータの型を指定する**Bcommand**メンバーが含まれています。 この仕様は、D3DDP2OP\_INDEXEDTRIANGLESTRIP などの[**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)列挙型の形式であり、テクスチャの状態を設定する場合は D3DDP2OP\_TEXTURESTAGESTATE です。

言い換えると、D3DHAL\_DP2OPERATION 操作コードでは、コマンドバッファー内の構造体の種類を指定します。 この後に続く構造体の数は、 **wPrimitiveCount**または**wstatecount**によって指定されます。共用体のメンバーは、D3DHAL\_DP2COMMAND 構造体のメンバーになります。 **WPrimitiveCount**メンバーは、レンダリングするグラフィックスプリミティブの数を追跡します。 **wstatecount**メンバーは、処理する状態変更の数を追跡します。

ドライバーが操作コードを処理する方法の例については、「[テクスチャステージの処理](processing-texture-stages.md)」を参照してください。

 

 





