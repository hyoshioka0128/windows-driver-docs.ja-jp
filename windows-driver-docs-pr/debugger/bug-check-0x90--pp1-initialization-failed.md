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
ms.openlocfilehash: dccd648aaac85477a8644719a2492899369cb5d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529825"
---
# <a name="bug-check-0x90-pp1initializationfailed"></a>バグのチェック 0x90:PP1\_初期化\_失敗


PP1\_初期化\_失敗のバグ チェックが 0x00000090 の値を持ちます。 このバグ チェックでは、プラグ アンド プレイ (PnP) マネージャーを初期化できなかったことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="pp1initializationfailed-parameters"></a>PP1\_初期化\_FAILED パラメーター


なし

<a name="cause"></a>原因
-----

カーネル モードの PnP マネージャーのフェーズ 1 の初期化中にエラーが発生しました。

フェーズ 1 では、それ以降の I/O の初期化中に呼び出すには、レジストリ ファイルの設定およびドライバーの場合は、その他の環境設定を含む、初期化の大部分を実行する場所です。

 

 




