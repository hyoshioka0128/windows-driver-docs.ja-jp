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
ms.openlocfilehash: 9b48b1f65ea54037489a5c8d99f3e234eb1f68f7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59904026"
---
# <a name="bug-check-0x16e-eresourceinvalidrelease"></a>バグ チェック 0x16E:スケジュール作成\_無効な\_リリース


スケジュール作成\_無効な\_リリースのバグ チェックが 0x0000016E の値を持ちます。 これは、ExReleaseResourceForThreadLite に指定されたターゲット スレッド ポインターが有効でないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


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

 

 




