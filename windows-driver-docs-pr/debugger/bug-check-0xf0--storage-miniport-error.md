---
title: Bug Check 0xF0 STORAGE_MINIPORT_ERROR
description: STORAGE_MINIPORT_ERROR のバグ チェックでは、0x00000F0 の値を持ちます。 ストレージ ミニポート ドライバーを SRB 要求を完了できなかったことを示します。
keywords:
- Bug Check 0xF0 STORAGE_MINIPORT_ERROR
- STORAGE_MINIPORT_ERROR
ms.date: 01/24/2019
topic_type:
- apiref
api_name:
- STORAGE_MINIPORT_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34250b9e7efac7ed20071b28e7634417e18c4cf3
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239210"
---
# <a name="bug-check-0xf0-storageminiporterror"></a>バグ チェック 0xF0:記憶域\_ミニポート\_エラー

記憶域\_ミニポート\_エラーのバグ チェックが 0x00000F0 の値を持ちます。 ストレージ ミニポート ドライバーを SRB 要求を完了できなかったことを示します。


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

 

## <a name="storageminiporterror-parameters"></a>記憶域\_ミニポート\_エラー パラメーター

|パラメーター|説明|
|-------- |---------- |
|1| エラー コード。 次の値を参照してください。|
|2| 次の値を参照してください。|
|3| 次の値を参照してください。|
|4| 次の値を参照してください。|

**値**

```text
1: Miniport failed to complete a SRB request even after successful reset operation.
    2 - Driver name unicode string address
    3 - SRB address
    4 - Storport unit device object

2: Miniport failed to complete a SRB request even after successful abort operation for the SRB.
    2 - Driver name unicode string address
    3 - Abort SRB address
    4 - SRB that was being aborted

3: Miniport failed to complete a request within a given timeout.
    2 - Driver name unicode string address
    3 - SRB address
    4 - Timeout of the request

4: Miniport failed to complete a request for a crypto operation. This can occur if it is trying to enable an encryption key on an ICE (Inline Crypto Engine) enabled UFS host. 
    2 - Driver name unicode string address
    3 - The STOR_CRYPTO_OPERATION_TYPE for this failure, typically StorCryptoOperationInsertKey
    4 - Reserved    
```


## <a name="cause"></a>原因
-----

記憶域ミニポート ドライバーのバグでは、完了 SRB 要求が保持されます。 エラーの特定の種類の上記のエラー コード値を参照してください。


## <a name="resolution"></a>解決方法
-----

[! 分析](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。 

2 番目のパラメーターで返されるドライバー名は、問題のあるドライバーを指す必要があります。


## <a name="see-also"></a>関連項目
----------

[バグチェック コード リファレンス](bug-check-code-reference2.md)

[Storport ミニポート ドライバー、Storport のインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-s-interface-with-storport-miniport-drivers)

