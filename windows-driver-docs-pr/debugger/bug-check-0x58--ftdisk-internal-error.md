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
ms.openlocfilehash: d5e83b1ff1a4cd851dce70b3c8a2f3ca7a7d131d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361821"
---
# <a name="bug-check-0x58-ftdiskinternalerror"></a>バグ チェック 0x58:FTDISK\_内部\_エラー


FTDISK\_内部\_エラーのバグ チェックが 0x00000058 の値を持ちます。 ミラー化されたパーティションの間違ったコピーから、システムが起動された場合に発行されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="ftdiskinternalerror-parameters"></a>FTDISK\_内部\_エラー パラメーター


なし

<a name="cause"></a>原因
-----

ミラーが有効ではありませんが、ハイブが示されます。 ハイブは、シャドウ パーティションに実際に指している必要があります。

これは、復元されているプライマリ パーティションによってほぼ常に発生します。

<a name="resolution"></a>解決方法
----------

シャドウのパーティションからシステムを再起動します。

 

 




