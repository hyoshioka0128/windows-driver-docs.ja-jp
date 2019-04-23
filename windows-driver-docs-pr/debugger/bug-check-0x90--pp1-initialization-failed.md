---
title: バグ チェック 0x90 PP1_INITIALIZATION_FAILED
description: PP1_INITIALIZATION_FAILED のバグ チェックでは、0x00000090 の値を持ちます。 このバグ チェックでは、プラグ アンド プレイ (PnP) マネージャーを初期化できなかったことを示します。
ms.assetid: 8dd46d24-0174-4310-953e-7b451ae34c71
keywords:
- バグ チェック 0x90 PP1_INITIALIZATION_FAILED
- PP1_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PP1_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7a1942cc86cd92cee35373855ff746c9afc215d8
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902824"
---
# <a name="bug-check-0x90-pp1initializationfailed"></a>バグ チェック 0x90:PP1\_初期化\_失敗


PP1\_初期化\_失敗のバグ チェックが 0x00000090 の値を持ちます。 このバグ チェックでは、プラグ アンド プレイ (PnP) マネージャーを初期化できなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="pp1initializationfailed-parameters"></a>PP1\_初期化\_FAILED パラメーター


なし

<a name="cause"></a>原因
-----

カーネル モードの PnP マネージャーのフェーズ 1 の初期化中にエラーが発生しました。

フェーズ 1 では、それ以降の I/O の初期化中に呼び出すには、レジストリ ファイルの設定およびドライバーの場合は、その他の環境設定を含む、初期化の大部分を実行する場所です。

 

 




