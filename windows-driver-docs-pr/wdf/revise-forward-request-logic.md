---
title: 転送要求のロジックを修正する
description: 転送要求のロジックを修正する
ms.assetid: B307AE04-7AA5-453D-9086-CD740617C659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e57e3a596a206fba678a652b099d8091812836da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325164"
---
# <a name="revise-forward-request-logic"></a>転送要求のロジックを修正する


ドライバーは、単独で要求を完了することはできません、[次へ] の下のドライバーに下位のスタックの要求が渡されます。 WDF のドライバーの場合、[次へ] の下のドライバーと見なされ、既定の I/O ターゲット WDFIOTARGET オブジェクトによって表されます。 ドライバーの呼び出しは、このオブジェクトを識別するハンドルを取得する[ **WdfDeviceGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff546017)します。

WDF のドライバーがスタックで、[次へ] の下のドライバーに要求を渡す方法については、次を参照してください。 [I/O 要求の転送](forwarding-i-o-requests.md)します。

 

 





