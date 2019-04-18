---
title: バグ チェック 0x20001 HYPERVISOR_ERROR
description: HYPERVISOR_ERROR のバグ チェックでは、0x00020001 の値を持ちます。 これは、ハイパーバイザーで致命的なエラーが発生したことを示します。
ms.assetid: 5F62DEEA-D192-46ED-827C-021A749D7091
keywords:
- バグ チェック 0x20001 HYPERVISOR_ERROR
- HYPERVISOR_ERROR
ms.date: 04/12/2019
topic_type:
- apiref
api_name:
- HYPERVISOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f01c98646698cc5b49881e5903b8d4a2960cdc35
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59745867"
---
# <a name="bug-check-0x20001-hypervisorerror"></a>バグ チェック 0x20001:ハイパーバイザー\_エラー


ハイパーバイザー\_エラーのバグ チェックが 0x00020001 の値を持ちます。 これは、ハイパーバイザーで致命的なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="hypervisorerror-parameters"></a>ハイパーバイザー\_エラー パラメーター


| パラメーター | 説明 |
|-----------|-------------|
| 1         | 予約済み    |
| 2         | 予約済み    |
| 3         | 予約済み    |
| 4         | 予約済み    |

## <a name="resolution"></a>解決方法 

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグし、根本原因を突き止めるに非常にすることができます。