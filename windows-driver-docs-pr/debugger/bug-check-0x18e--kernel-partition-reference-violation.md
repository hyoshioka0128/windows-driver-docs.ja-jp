---
title: バグ チェック 0x18E KERNEL_PARTITION_REFERENCE_VIOLATION
description: KERNEL_PARTITION_REFERENCE_VIOLATION のバグ チェックでは、0x0000018E の値を持ちます。
keywords:
- バグ チェック 0x18E KERNEL_PARTITION_REFERENCE_VIOLATION
- KERNEL_PARTITION_REFERENCE_VIOLATION
ms.date: 05/23/2018
topic_type:
- apiref
api_name:
- KERNEL_PARTITION_REFERENCE_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86603fb969f95ccf0fcf875a517f4e8abcc8f2b7
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519839"
---
# <a name="bug-check-bug-check-0x18e-kernelpartitionreferenceviolation"></a>チェックのバグ チェック 0x18E をバグします。カーネル\_パーティション\_参照\_違反

KERNEL_PARTITION_REFERENCE_VIOLATION のバグ チェックでは、0x0000018E の値を持ちます。 

このエラーは、パーティションが正しく逆参照されることを示します。 これは通常、カーネル モード ドライバーはパーティション オブジェクトを逆参照正しくときに発生します。 また、カーネルの重大なデータ破損が発生したときにも発生することができます。


> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="kernelpartitionreferenceviolation-parameters"></a>カーネル\_パーティション\_参照\_違反パラメーター

次のパラメーターは、ブルー スクリーンに表示されます。

パラメーター 1 では、エラーの種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

パラメーター 1 | パラメータ 2 | 3 番目のパラメーター | パラメーター 4
|-----------|-------------|-------------|-------------|
| 0x0 :パーティション数は 0 以外の強い参照を削除しています。 | パーティションへのポインター。 | ハードの未解決の参照の数。 | 予約済み|
| 0x1:システム パーティションを削除しています | パーティションへのポインター。 | 予約済み | 予約済み |
| 0x2:未処理の例: 作業項目をキューのパーティションを削除しています。 | パーティションへのポインター。 |Ex へのポインターには、未処理の項目を含むキューが動作します。 | 予約済み |
 






