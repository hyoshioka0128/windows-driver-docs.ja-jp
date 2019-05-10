---
title: Bug Check 0x1D3 WFP_INVALID_OPERATION
description: WFP_INVALID_OPERATION のバグ チェックでは、0x000001D3 の値を持ちます。
keywords:
- Bug Check 0x1D3 WFP_INVALID_OPERATION
- WFP_INVALID_OPERATION
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- WFP_INVALID_OPERATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f03d89fdc91e77388418b182ac7200817091ff3
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106383"
---
# <a name="bug-check-bug-check-0x1d3-wfpinvalidoperation"></a>チェックのバグ チェック 0x1D3 をバグします。WFP_INVALID_OPERATION 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


WFP_INVALID_OPERATION のバグ チェックでは、0x000001D3 の値を持ちます。 これは、Windows フィルタ リング プラットフォームのコールアウトが無効な操作を実行することを示します。

## <a name="wfpinvalidoperation-parameters"></a>WFP\_無効な\_操作のパラメーター

パラメーター | 説明 
|---------|--------------|
1 | バグチェックのサブタイプ。
2 | 予約済み
3 | 予約済み
4 | 予約済み


**パラメーター 1 の値**

 0x1:引き出し線の挿入、NBL 複数 NET_BUFFERS を受信します。

  2-予約されています。

  3 - NBL へのポインター。

  4-予約されています。


## <a name="resolution"></a>解決方法
[ **! 分析**](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。

 




