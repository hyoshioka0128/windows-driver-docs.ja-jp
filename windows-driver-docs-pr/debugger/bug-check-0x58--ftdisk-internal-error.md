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
ms.openlocfilehash: 0bc8c9bd495d6780aac4dc5a65bfe512ffbc486c
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903257"
---
# <a name="bug-check-0x58-ftdiskinternalerror"></a>バグ チェック 0x58:FTDISK\_内部\_エラー


FTDISK\_内部\_エラーのバグ チェックが 0x00000058 の値を持ちます。 ミラー化されたパーティションの間違ったコピーから、システムが起動された場合に発行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="ftdiskinternalerror-parameters"></a>FTDISK\_内部\_エラー パラメーター


なし

<a name="cause"></a>原因
-----

ミラーが有効ではありませんが、ハイブが示されます。 ハイブは、シャドウ パーティションに実際に指している必要があります。

これは、復元されているプライマリ パーティションによってほぼ常に発生します。

<a name="resolution"></a>解決方法
----------

シャドウのパーティションからシステムを再起動します。

 

 




