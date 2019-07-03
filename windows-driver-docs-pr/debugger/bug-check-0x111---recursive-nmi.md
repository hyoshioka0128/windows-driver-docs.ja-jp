---
title: バグ チェック 0x111 RECURSIVE_NMI
description: RECURSIVE_NMI のバグ チェックでは、0x00000111 の値を持ちます。 このバグ チェックでは、前の NMI の処理中に、非マスク-割り込み (NMI) が発生したことを示します。
ms.assetid: 1f275db1-ac79-4bd2-85c5-cb64342911d1
keywords:
- バグ チェック 0x111 RECURSIVE_NMI
- RECURSIVE_NMI
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RECURSIVE_NMI
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb606d9ecc12428a3601fe5dc48907222b7f8e24
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521247"
---
# <a name="bug-check-0x111-recursivenmi"></a>バグ チェック 0x111:再帰的な\_NMI


再帰的な\_NMI バグ チェックが 0x00000111 の値を持ちます。 このバグ チェックでは、前の NMI の処理中に、非マスク-割り込み (NMI) が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


<a name="remarks"></a>注釈
-------

このバグ チェックは、システム管理の割り込み (SMI) コードでエラーがあると、SMI は、NMI を中断し、割り込みを有効に発生します。 有効になっている、Nmi とし、実行が継続し、別 NMI が進行中の NMI を中断します。

 

 




