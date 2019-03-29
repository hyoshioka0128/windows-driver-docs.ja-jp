---
title: Bug Check 0x170 CRYPTO_LIBRARY_INTERNAL_ERROR
description: CRYPTO_LIBRARY_INTERNAL_ERROR のバグ チェックでは、0x00000170 の値を持ちます。 暗号化ライブラリで内部エラーが発生したことを示します。
keywords:
- Bug Check 0x170 CRYPTO_LIBRARY_INTERNAL_ERROR
- CRYPTO_LIBRARY_INTERNAL_ERROR
ms.date: 01/10/2019
topic_type:
- apiref
api_name:
- CRYPTO_LIBRARY_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f54fa6836b8c7efff2729268e577ca9388a2406b
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743527"
---
# <a name="bug-check-0x170-cryptolibraryinternalerror"></a>バグ チェック 0x170 の。CRYPTO\_ライブラリ\_内部\_エラー 

CRYPTO\_ライブラリ\_内部\_エラーのバグ チェックが 0x00000170 の値を持ちます。 暗号化ライブラリで内部エラーが発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


 ## <a name="cryptolibraryinternalerror--parameters"></a>CRYPTO\_ライブラリ\_内部\_エラー パラメーター

|パラメーター|説明|
|--- |--- |
|1| エラーの ID。|
|2| 予約済み。|
|3| 予約済み。 |
|4| 予約済み。 |


## <a name="cause"></a>原因
-----

このバグチェックは、暗号化ライブラリ ヒットが発生することはありませんが、異常とライブラリが安全なメソッドの呼び出し元にエラーが通知を持たないを示します。  アクティブな攻撃の兆候があります。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

[Cryptography API:次世代](https://docs.microsoft.com/windows/desktop/SecCNG/cng-portal) 


