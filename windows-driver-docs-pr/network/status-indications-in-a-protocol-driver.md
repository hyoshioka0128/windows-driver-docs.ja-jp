---
title: プロトコル ドライバーの状態表示
description: プロトコル ドライバーの状態表示
ms.assetid: 4b0426bb-4311-4251-b9ee-38d081f061e5
keywords:
- プロトコル ドライバー WDK ネットワー キング、状態インジケーター
- NDIS プロトコル ドライバー WDK、状態インジケーター
- 状態インジケーターの WDK ネットワー キング、プロトコル ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ce4879c16da977dcf9d8b3ca55aa3f09c7e9e4c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573609"
---
# <a name="status-indications-in-a-protocol-driver"></a>プロトコル ドライバーの状態表示





プロトコル ドライバーに状態インジケーターの 2 つの異なるインターフェイスがあります。 コネクションレスの下端との NDIS プロトコル ドライバーを指定するために必要な[ **ProtocolStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570270)関数。 NDIS 呼び出し*ProtocolStatusEx*基になるコネクションレス ミニポート ドライバーを呼び出すと[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)そのハードウェアの状態の変更を報告します。 NDIS 呼び出し*ProtocolStatusEx*状態の変更を開始するとき。 コネクションレスのプロトコル ドライバーに状態インジケーターの詳細については、[プロトコル ドライバーに状態インジケーターの処理](handling-status-indications-in-a-protocol-driver.md)を参照してください。

接続指向プロトコル ドライバーを指定する必要があります、 [ **ProtocolCoStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff570258)関数。 NDIS 呼び出し*ProtocolCoStatusEx*を基になる接続指向のミニポート ドライバーを呼び出すと[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)そのハードウェアの状態の変更を報告するには. NDIS 呼び出し*ProtocolCoStatusEx*状態の変更を開始するとき。 接続指向プロトコル ドライバーに状態インジケーターの詳細については、次を参照してください[Connection-Oriented 操作。](connection-oriented-operations.md)

可能な状態インジケーターの完全な一覧を参照してください。[状態インジケーター](https://msdn.microsoft.com/library/windows/hardware/ff570879)します。

 

 





