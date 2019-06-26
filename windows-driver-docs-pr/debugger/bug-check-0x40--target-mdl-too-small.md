---
title: バグ チェック 0x40 TARGET_MDL_TOO_SMALL
description: TARGET_MDL_TOO_SMALL のバグ チェックでは、0x00000040 の値を持ちます。 これは、ドライバーが IoBuildPartialMdl を正しく使用することを示します。
ms.assetid: bd154c1f-6c74-424e-bc32-22c9a93efae5
keywords:
- バグ チェック 0x40 TARGET_MDL_TOO_SMALL
- TARGET_MDL_TOO_SMALL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TARGET_MDL_TOO_SMALL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aea99c33cb3288a4141238140b95a8628452d0c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361881"
---
# <a name="bug-check-0x40-targetmdltoosmall"></a>バグ チェック 0x40:ターゲット\_MDL\_すぎます\_小さな


ターゲット\_MDL\_すぎます\_小さなバグ チェックが 0x00000040 の値を持ちます。 これは、ドライバーが正しく使用されていることを示します**IoBuildPartialMdl**します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="targetmdltoosmall-parameters"></a>ターゲット\_MDL\_すぎます\_小さなパラメーター


なし

<a name="cause"></a>原因
-----

これは、ドライバーのバグです。 ドライバーが呼び出されて、 **IoBuildPartialMdl**関数を渡して、MDL MDL、ソースの一部が MDL が要求されたアドレスの範囲全体をマップするのに十分な大きさでは、ターゲットをマップします。

<a name="resolution"></a>解決方法
----------

1、2、および 4 番目の引数には、ソースとターゲット MDLs、だけでなく、アドレス範囲の長さをマップできる、 **IoBuildPartialMdl**関数。 そのため、この特定の関数のスタック トレースを行うは、デバッグ プロセス中に役立つ可能性があります。 コードが正しくターゲット MDL のこの関数に渡すアドレス範囲の長さのために必要なサイズを計算することを確認します。

 

 




