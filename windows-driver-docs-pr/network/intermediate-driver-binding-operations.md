---
title: 中間ドライバー バインド操作
description: 中間ドライバー バインド操作
ms.assetid: 129a744c-d4d4-4741-9812-e76087c585fc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f7d9c30b1d75b611caf4f3e4e1f2686b3f76c53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377886"
---
# <a name="intermediate-driver-binding-operations"></a>中間ドライバー バインド操作





NDIS を呼び出すミニポート アダプターが使用可能になるときに、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)そのミニポート アダプターにバインドできる任意の中間ドライバーの関数。

中間のドライバー提供プロトコル バインディング操作を記載する必要があります[をアダプターにバインド](binding-to-an-adapter.md)します。

バインディング時のアクションには、割り当てのアダプター固有のコンテキスト バインディングの領域を初期化し、仮想のミニポートの初期化、および呼び出しが含まれます[ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715)にバインドする、。アダプター。

中間のドライバーが個別に割り当てる必要はありません[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)バインディングごとにプールを構成します。 NET の割り当てに必要な中間ドライバー\_バッファー\_ドライバー デザインでは、独自の構造を割り当てることが必要な場合にのみプールの一覧の構造体。 それ以外の場合、ドライバーでは、他のドライバーから受信された構造に渡すことができますだけです。 このようなドライバーは、送信のための別のプールを割り当てるし、受信する必要があります。

割り当てし、ネットワークのデータを管理するための要件については、次を参照してください。[中間ドライバー ネットワーク データ管理](intermediate-driver-network-data-management.md)します。

 

 





