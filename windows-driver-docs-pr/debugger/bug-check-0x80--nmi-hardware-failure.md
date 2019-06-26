---
title: バグ チェック 0x80 NMI_HARDWARE_FAILURE
description: NMI_HARDWARE_FAILURE のバグ チェックでは、0x00000080 の値を持ちます。 このバグ チェックでは、ハードウェアの故障が発生したことを示します。
ms.assetid: 1b376540-d101-44af-8295-d8078a920c67
keywords:
- バグ チェック 0x80 NMI_HARDWARE_FAILURE
- NMI_HARDWARE_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NMI_HARDWARE_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 121fe1dfd53060487ff617106413825b90d4af7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361732"
---
# <a name="bug-check-0x80-nmihardwarefailure"></a>バグ チェック 0x80:NMI\_ハードウェア\_エラー


NMI\_ハードウェア\_エラーのバグ チェックが 0x00000080 の値を持ちます。 このバグ チェックでは、ハードウェアの故障が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="nmihardwarefailure-parameters"></a>NMI\_ハードウェア\_エラー パラメーター


なし

<a name="cause"></a>原因
-----

さまざまなハードウェアの故障する可能性 NMI\_ハードウェア\_エラーのバグ チェック。 正確な原因は特定が困難にします。

<a name="resolution"></a>解決方法
----------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。 すべてのハードウェアや最近インストールされたドライバーを削除します。 メモリのすべてのモジュールは、同じ型のことを確認します。

 

 




