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
ms.openlocfilehash: a55dbebcc53e18aa328985079a034da07c358c9c
ms.sourcegitcommit: fac288eb2cceb6a7a8248ae0f8086553d1659b23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56588957"
---
# <a name="bug-check-0x80-nmihardwarefailure"></a>バグ チェック 0x80:NMI\_ハードウェア\_エラー


NMI\_ハードウェア\_エラーのバグ チェックが 0x00000080 の値を持ちます。 このバグ チェックでは、ハードウェアの故障が発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="nmihardwarefailure-parameters"></a>NMI\_ハードウェア\_エラー パラメーター


なし

<a name="cause"></a>原因
-----

さまざまなハードウェアの故障する可能性 NMI\_ハードウェア\_エラーのバグ チェック。 正確な原因は特定が困難にします。

<a name="resolution"></a>解決方法
----------

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。 すべてのハードウェアや最近インストールされたドライバーを削除します。 メモリのすべてのモジュールは、同じ型のことを確認します。

 

 




