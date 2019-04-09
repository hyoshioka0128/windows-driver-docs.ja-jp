---
title: バグ チェック 0x1CB INVALID_SILO_DETACH
description: INVALID_SILO_DETACH のバグ チェックでは、0x000001CB の値を持ちます。 スレッドが終了する前に、サイロからデタッチが失敗したことを示します。
keywords:
- バグ チェック 0x1CB INVALID_SILO_DETACH
- INVALID_SILO_DETACH
ms.date: 02/21/2019
topic_type:
- apiref
api_name:
- INVALID_SILO_DETACH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e228b443f8214e878b2158db80d3239cf2d761db
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239835"
---
# <a name="bug-check-0x1cb-invalidsilodetach"></a>バグ チェック 0x1CB:無効な\_サイロ\_デタッチ

無効な\_サイロ\_デタッチのバグ チェックが 0x000001CB の値を持ちます。 スレッドが終了する前に、サイロからデタッチが失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 

## <a name="invalidsilodetach-parameters"></a>無効な\_サイロ\_デタッチ パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| 接続されているスレッドへのポインター。 |
|2| 以前サイロにアタッチされています。 |
|3| スレッドのプロセスへのポインター。 |
|4| 予約済み。 |


## <a name="cause"></a>原因
-----
スレッドを終了する前に、サイロからデタッチできませんでした。 



## <a name="see-also"></a>関連項目
----------

[バグ チェック コード リファレンス](bug-check-code-reference2.md)

