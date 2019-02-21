---
title: 要求を転送するロジックを修正します。
description: 要求を転送するロジックを修正します。
ms.assetid: B307AE04-7AA5-453D-9086-CD740617C659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e57e3a596a206fba678a652b099d8091812836da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549199"
---
# <a name="revise-forward-request-logic"></a>要求を転送するロジックを修正します。


ドライバーは、単独で要求を完了することはできません、[次へ] の下のドライバーに下位のスタックの要求が渡されます。 WDF のドライバーの場合、[次へ] の下のドライバーと見なされ、既定の I/O ターゲット WDFIOTARGET オブジェクトによって表されます。 ドライバーの呼び出しは、このオブジェクトを識別するハンドルを取得する[ **WdfDeviceGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff546017)します。

WDF のドライバーがスタックで、[次へ] の下のドライバーに要求を渡す方法については、次を参照してください。 [I/O 要求の転送](forwarding-i-o-requests.md)します。

 

 





