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
ms.openlocfilehash: f69fb24bc593500937100c4d0e84c8f5bdd237ef
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519609"
---
# <a name="bug-check-0x20001-hypervisorerror"></a>バグ チェック 0x20001:ハイパーバイザー\_エラー


ハイパーバイザー\_エラーのバグ チェックが 0x00020001 の値を持ちます。 これは、ハイパーバイザーで致命的なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。

## <a name="hypervisorerror-parameters"></a>ハイパーバイザー\_エラー パラメーター


| パラメーター | 説明 |
|-----------|-------------|
| 1         | 予約済み    |
| 2         | 予約済み    |
| 3         | 予約済み    |
| 4         | 予約済み    |

## <a name="resolution"></a>解決方法 

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグし、根本原因を突き止めるに非常にすることができます。