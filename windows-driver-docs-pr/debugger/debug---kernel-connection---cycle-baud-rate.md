---
title: カーネルの接続をデバッグ サイクル ボー レート
description: カーネルの接続をデバッグ サイクル ボー レート
ms.assetid: 5d7f13ff-738d-498c-88cb-ad2d6fe596ac
keywords:
- カーネルの接続をデバッグ サイクル ボー レート
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f611063e3a6207db1cddb9017b08b2a3bf9a21d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571364"
---
# <a name="debug--kernel-connection--cycle-baud-rate"></a>Debug | Kernel Connection | Cycle Baud Rate (デバッグ | カーネル接続 | ボーレートを切り替える)


## <span id="ddk_debug_kernel_connection_cycle_baud_rate_dbg"></span><span id="DDK_DEBUG_KERNEL_CONNECTION_CYCLE_BAUD_RATE_DBG"></span>


をポイント**カーネル接続**順にクリックします**サイクル ボー レート**上、**デバッグ**カーネル デバッグ接続で使用するボー レートを変更するメニュー。

このコマンドは、CTRL + ALT + A キーを押すと同じです。 (することができますも押して CTRL + A KD で)。

このコマンドは、接続をデバッグするカーネル用のすべての利用可能なボー レートを循環します。 サポートされているボー レートは 38400、19200、57600、および 115200 です。 次のコマンドを使用するたびに、[次へ] のボー レートが選択されます。 ボー レートの 115200 が既には 19200 減少します。

このコマンドを使用して、ボー レートをデバッグする位置を変更することはできません。 ホスト コンピューターと対象コンピューターのボー レートが一致する必要があり、コンピューターを再起動せず、ターゲット コンピューターのボー レートを変更することはできません。 したがって、2 台のコンピューターが異なるレートで通信するためにしようとした場合にのみ、ボー レートを変更する必要があります。 この場合、ターゲット コンピューターの一致するように、ホスト コンピューターのボー レートを変更する必要があります。

 

 





