---
title: バグ チェック 0x149 REFS_FILE_SYSTEM
description: REFS_FILE_SYSTEM のバグ チェックでは、0x00000149 の値を持ちます。 これは、ファイル システム エラーが発生したことを示します。
ms.assetid: 899E89E7-46CD-4143-B1DC-7959F01643CF
keywords:
- バグ チェック 0x149 REFS_FILE_SYSTEM
- REFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 59b75b6fdfbafeeb879651b8cceef5cc007d08f8
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902278"
---
# <a name="bug-check-0x149-refsfilesystem"></a>バグ チェック 0x149:REFS\_ファイル\_システム


REFS\_ファイル\_システムのバグ チェックが 0x00000149 の値を持ちます。 これは、ファイル システム エラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="refsfilesystem-parameters"></a>REFS\_ファイル\_システム パラメーター


| パラメーター | 説明                          |
|-----------|--------------------------------------|
| 1         | \_\_行\_\_                         |
| 2         | ExceptionRecord                      |
| 3         | ContextRecord                        |
| 4         | ExceptionRecord-&gt;ExceptionAddress |

 

| パラメーター | 説明 |
|-----------|-------------|
| 1         | メッセージ     |
| 2         | 予約済み    |
| 3         | 予約済み    |
| 4         | 予約済み    |

 

<a name="resolution"></a>解決方法
----------

スタックに RefsExceptionFilter を参照してください例外レコードとコンテキスト レコードの 2 番目と 3 番目のパラメーターが、します。 [ **.Exr** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-exr--display-exception-record-)例外情報を表示する 2 番目のパラメーターで実行し、 [ **.cxr** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-cxr--display-context-record-)第 3 パラメーターと[**kb** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)有益なスタック トレースを取得します。

 

 




