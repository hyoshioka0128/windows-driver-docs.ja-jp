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
ms.openlocfilehash: d330fe593c297a41ab575a65dc0cf4f23d28f741
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358188"
---
# <a name="bug-check-0x111-recursivenmi"></a>バグ チェック 0x111:再帰的な\_NMI


再帰的な\_NMI バグ チェックが 0x00000111 の値を持ちます。 このバグ チェックでは、前の NMI の処理中に、非マスク-割り込み (NMI) が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


<a name="remarks"></a>注釈
-------

このバグ チェックは、システム管理の割り込み (SMI) コードでエラーがあると、SMI は、NMI を中断し、割り込みを有効に発生します。 有効になっている、Nmi とし、実行が継続し、別 NMI が進行中の NMI を中断します。

 

 




