---
title: バグ チェック 0x58 FTDISK_INTERNAL_ERROR
description: FTDISK_INTERNAL_ERROR のバグ チェックでは、0x00000058 の値を持ちます。 ミラー化されたパーティションの間違ったコピーから、システムが起動された場合に発行されます。
ms.assetid: c8de6a04-740d-415e-bf23-b28da066a225
keywords:
- バグ チェック 0x58 FTDISK_INTERNAL_ERROR
- FTDISK_INTERNAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FTDISK_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 72d593051e396998d7c71bf73e5f9a0391dfdc39
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519355"
---
# <a name="bug-check-0x58-ftdiskinternalerror"></a>バグ チェック 0x58:FTDISK\_内部\_エラー


FTDISK\_内部\_エラーのバグ チェックが 0x00000058 の値を持ちます。 ミラー化されたパーティションの間違ったコピーから、システムが起動された場合に発行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="ftdiskinternalerror-parameters"></a>FTDISK\_内部\_エラー パラメーター


なし

<a name="cause"></a>原因
-----

ミラーが有効ではありませんが、ハイブが示されます。 ハイブは、シャドウ パーティションに実際に指している必要があります。

これは、復元されているプライマリ パーティションによってほぼ常に発生します。

<a name="resolution"></a>解決方法
----------

シャドウのパーティションからシステムを再起動します。

 

 




