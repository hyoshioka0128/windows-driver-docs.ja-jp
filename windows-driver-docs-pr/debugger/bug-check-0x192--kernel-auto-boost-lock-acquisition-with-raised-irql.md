---
title: バグ チェック 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
description: KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL のバグ チェックでは、DISPATCH_LEVEL 以上を実行中に AutoBoost によって追跡されるロックが取得されたことを示します。
ms.assetid: D88EF2CC-26DC-44D8-80CB-18D058C6A413
keywords:
- バグ チェック 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b71a6f292ad0688962b2001a941b1b3a6382bbe
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519829"
---
# <a name="bug-check-0x192-kernelautoboostlockacquisitionwithraisedirql"></a>バグ チェック 0x192:カーネル\_自動\_BOOST\_ロック\_買収\_WITH\_発生\_IRQL


カーネル\_自動\_BOOST\_ロック\_買収\_WITH\_発生\_IRQL のバグ チェックが 0x00000192 の値を持ちます。 これは、ディスパッチで実行中に AutoBoost によって追跡されるロックが取得されたことを示します\_レベルまたはそれ以降。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="kernelautoboostlockacquisitionwithraisedirql-parameters"></a>カーネル\_自動\_BOOST\_ロック\_買収\_WITH\_発生\_IRQL パラメーター


| パラメーター | 説明                             |
|-----------|-----------------------------------------|
| 1         | スレッドのアドレス               |
| 2         | ロックのアドレス                        |
| 3         | ロックが取得された IRQL |
| 4         | 予約済み                                |

 

<a name="cause"></a>原因
-----

APC の上のロックを呼び出し元をブロックすることはできません\_レベルため、デッドロックの原因となる割り込まれたスレッドによって排他的ロックが保持されることもできます。

 

 




