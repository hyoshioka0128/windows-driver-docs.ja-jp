---
title: バグ チェック 0x16E ERESOURCE_INVALID_RELEASE
description: ERESOURCE_INVALID_RELEASE のバグ チェックでは、0x0000016E の値を持ちます。 これは、ExReleaseResourceForThreadLite に指定されたターゲット スレッド ポインターが有効でないことを示します。
ms.assetid: F180D28D-70B7-4E78-9E04-C5DC19A41EB9
keywords:
- バグ チェック 0x16E ERESOURCE_INVALID_RELEASE
- ERESOURCE_INVALID_RELEASE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ERESOURCE_INVALID_RELEASE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7a01dc5ab68150cde4ddf60efc67b3bdc9cb47a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548981"
---
# <a name="bug-check-0x16e-eresourceinvalidrelease"></a>バグ チェック 0x16E の。スケジュール作成\_無効な\_リリース


スケジュール作成\_無効な\_リリースのバグ チェックが 0x0000016E の値を持ちます。 これは、ExReleaseResourceForThreadLite に指定されたターゲット スレッド ポインターが有効でないことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="eresourceinvalidrelease-parameters"></a>スケジュール作成\_無効な\_リリース パラメーター


| パラメーター | 説明                                    |
|-----------|------------------------------------------------|
| 1         | リリースされているリソース                    |
| 2         | 現在のスレッド                             |
| 3         | 渡された無効なターゲット スレッド |
| 4         | 予約済み                                       |

 

<a name="cause"></a>原因
-----

(この場合、スレッド間のリリースの対象としていますが) ExSetOwnerPointerEx への呼び出しは、API クライアントでスキップされましたか、呼び出し元が誤って指定したその他の値で渡された場合、このバグチェックがヒット ExGetCurrentResourceThread でします。

 

 




