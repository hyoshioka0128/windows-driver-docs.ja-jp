---
title: ストリーム ポインター タイマー
description: ストリーム ポインター タイマー
ms.assetid: 98413fc6-2b62-4c52-9ac4-bd2a3a60db60
keywords:
- ストリームポインター WDK AVStream、タイマー
- タイマー WDK AVStream
- タイムアウト WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3773e0ca6019315bf73d0c780227c852c2a152f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837679"
---
# <a name="stream-pointer-timers"></a>ストリーム ポインター タイマー





ストリームポインターにタイマーを設定するには、 [**Ksk streampointer Scheduletimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerscheduletimeout)を呼び出します。 指定されたストリームポインター*が有効期限*までに削除されていない場合、avstream は、ベンダーが提供するタイマーコールバックルーチンを呼び出します。 *間隔*を100ナノ秒単位で指定します。

タイムアウトを取り消すには、 [**Ksstreamポインター Canceltimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointercanceltimeout)を呼び出します。

 

 




