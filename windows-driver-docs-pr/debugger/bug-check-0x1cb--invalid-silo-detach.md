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
ms.openlocfilehash: 15300ced5761c3bcbee29a6a29fd0938a9abc54f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367617"
---
# <a name="bug-check-0x1cb-invalidsilodetach"></a>バグ チェック 0x1CB:無効な\_サイロ\_デタッチ

無効な\_サイロ\_デタッチのバグ チェックが 0x000001CB の値を持ちます。 スレッドが終了する前に、サイロからデタッチが失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。

 

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

[バグチェック コード リファレンス](bug-check-code-reference2.md)

