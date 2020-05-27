---
title: バグチェック 0x18E KERNEL_PARTITION_REFERENCE_VIOLATION
description: KERNEL_PARTITION_REFERENCE_VIOLATION バグチェックの値は0x0000018E です。
keywords:
- バグチェック 0x18E KERNEL_PARTITION_REFERENCE_VIOLATION
- KERNEL_PARTITION_REFERENCE_VIOLATION
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- KERNEL_PARTITION_REFERENCE_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0142d57396cc4e980a30a7b4264970e5ecc67647
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852318"
---
# <a name="bug-check-0x18e-kernel_partition_reference_violation"></a>バグチェック 0x18E: カーネル \_ パーティションの \_ 参照 \_ 違反

KERNEL_PARTITION_REFERENCE_VIOLATION バグチェックの値は0x0000018E です。 

このエラーは、パーティションが正しく逆参照されなかったことを示します。 これは通常、カーネルモードドライバーがパーティションオブジェクトを適切に逆参照しない場合に発生します。 また、カーネルで重大なデータ破損が発生した場合にも発生する可能性があります。


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="kernel_partition_reference_violation-parameters"></a>カーネル \_ パーティション \_ 参照 \_ 違反パラメーター

次のパラメーターがブルースクリーンに表示されます。

パラメーター1はエラーの種類を示します。 他のパラメーターの意味は、パラメーター1の値によって異なります。

パラメーター 1 | パラメータ 2 | パラメーター3 | パラメーター4
|-----------|-------------|-------------|-------------|
| 0x0: ハード参照カウントが0でないパーティションが削除されています。 | パーティションへのポインター。 | 未解決のハード参照の数。 | 予約済み|
| 0x1: システムパーティションが削除されています | パーティションへのポインター。 | 予約済み | 予約済み |
| 0x2: 未完了の ex work queue 項目を含むパーティションが削除されています。 | パーティションへのポインター。 |未処理の項目を含む ex work キューへのポインター。 | 予約済み |
 






