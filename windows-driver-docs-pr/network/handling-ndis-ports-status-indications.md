---
title: NDIS ポート状態表示の処理
description: NDIS ポート状態表示の処理
ms.assetid: ba3794de-b17e-4878-a65e-6c9f5f8ebbbc
keywords:
- WDK NDIS、状態インジケーターをポートします。
- NDIS ポート WDK、状態インジケーター
- 状態インジケーターの WDK ネットワー キング、NDIS ポート
- ポートの状態が WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa2736700309636b757f6c01e149a5ec037127f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347330"
---
# <a name="handling-ndis-ports-status-indications"></a>NDIS ポート状態表示の処理





ミニポート ドライバーを使用する必要があります、NDIS ポートが状態表示のソースの場合は、 **PortNumber**内のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)ソース ポートを指定する構造体。 ミニポート ドライバーは、決して非アクティブなポートの状態を示します。

ミニポート ドライバーを使用する必要があります、 [ **NDIS\_状態\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567415) NDIS ポートの状態の変化を示すステータスを示す値。 この状態表示のミニポート ドライバーでポート番号を設定する必要があります、 **PortNumber**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。 **StatusBuffer**の NDIS メンバー\_状態\_を示す値構造体にはへのポインターが含まれています、 [ **NDIS\_ポート\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff566800)構造体。

 

 





