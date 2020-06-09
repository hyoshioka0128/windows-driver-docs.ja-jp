---
title: バグチェック 0x1D3 WFP_INVALID_OPERATION
description: WFP_INVALID_OPERATION のバグチェックには、0x000001D3 という値が指定されています。
keywords:
- バグチェック 0x1D3 WFP_INVALID_OPERATION
- WFP_INVALID_OPERATION
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- WFP_INVALID_OPERATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 04fb86d17a3a4d0aa3d7655d04965151ca0e1db1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534833"
---
# <a name="bug-check-0x1d3-wfp_invalid_operation"></a>バグ チェック 0x1D3:WFP_INVALID_OPERATION 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


WFP_INVALID_OPERATION のバグチェックには、0x000001D3 という値が指定されています。 これは、Windows フィルタリングプラットフォームのコールアウトが無効な操作を実行したことを示します。

## <a name="wfp_invalid_operation-parameters"></a>WFP の \_ 無効な \_ 操作パラメーター

パラメーター | 説明 
|---------|--------------|
1 | バグチェックのサブタイプ。
2 | 予約済み
3 | 予約済み
4 | 予約済み

**パラメーター1の値**

 0x1: コールアウトによって、複数の NET_BUFFERS 受信を含む NBL が挿入されます。

 2-予約済み。

 3-NBL へのポインター。

 4-予約済み。


## <a name="resolution"></a>解像度
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに非常に役立ちます。

 




