---
title: Bug Check 0x1D7 EFS_FATAL_ERROR
description: EFS_FATAL_ERROR のバグ チェックでは、0x000001D7 の値を持ちます。 データ損失やデータの破損なしに処理できないように、EFS のエラー条件が発生したことを示します。
keywords:
- Bug Check 0x1D7 EFS_FATAL_ERROR
- EFS_FATAL_ERROR
ms.date: 01/22/2019
topic_type:
- apiref
api_name:
- EFS_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e2a2d19e10d2e4684412db578727f0292e5e73f2
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519637"
---
# <a name="bug-check-0x1d7-efsfatalerror"></a>バグ チェック 0x1D7:EFS\_FATAL\_エラー

EFS\_FATAL\_エラーのバグ チェックが 0x000001D7 の値を持ちます。 データ損失やデータの破損なしに処理できないように、EFS のエラー条件が発生したことを示します。


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。

 

## <a name="efsfatalerror-parameters"></a>EFS\_FATAL\_エラー パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| バグ チェック サブクラスです。**01** -障害を事前にオフロードします。|
|2| NTSTATUS には、操作のコードが返されます。|
|3| エラー発生時に現在 IRP します。|
|4| エラー発生時にファイル暗号化コンテキスト。|

## <a name="cause"></a>原因
-----

データ損失やデータの破損なしに処理できないように、EFS のエラー条件が発生しました。

## <a name="resolution"></a>解決方法
-----

[! 分析](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

2 番目のパラメーターを試して、NT_SUCCESS がいないに返された理由を確認 NTSTATUS フィールドを確認します。 これは、予想されるのみ許容値はファイル システムの暗号化済みのオフロードを呼び出すことです。

デバッガーを使用して[!IRP](-irp.md)パラメーター 3 の考えられるの競合する IRP コードまたはその他の問題を調査するコマンド。



## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

