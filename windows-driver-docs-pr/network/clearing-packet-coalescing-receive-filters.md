---
title: パケット結合受信フィルターのクリア
description: パケット結合受信フィルターのクリア
ms.assetid: 0924A494-AA4E-45FA-AFE6-65E0D105E0F2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f3a26d7119945727ff823679026543958be4aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353276"
---
# <a name="clearing-packet-coalescing-receive-filters"></a>パケット結合受信フィルターのクリア


を解放するまたは*オフ*、パケットの結合をサポートしているミニポート ドライバーに対する受信フィルター、上位のドライバーがの OID セット要求を発行する[OID\_受信\_フィルター\_オフ\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569785)します。 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体にはへのポインターが含まれています、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567166)構造体。

プロトコルまたはフィルター ドライバーなど、上にあるドライバーを初期化します、 [ **NDIS\_受信\_フィルター\_クリア\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff567166)構造体次のように

-   **QueueId** NDIS にメンバーを設定する必要があります\_既定\_受信\_キュー\_id。

    **注**  NDIS 6.30 以降では、フィルターが受信パケットの結合は、既定でのみサポートの受信ネットワーク アダプターのキュー。 この受信キューが識別子の NDIS\_既定\_受信\_キュー\_id。

     

-   **FilterId**メンバーする必要がありますを設定する、0 以外の識別子 (ID)、ミニポート ドライバーにクリアするフィルターの値。 上にあるドライバーの以前の OID メソッド要求から、フィルター ID を取得した[OID\_受信\_フィルター\_設定\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569795)または[OID\_受信\_フィルター\_ENUM\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569787)します。

    **注**  だけで受信のフィルターをパケットの結合セット上にあるドライバーがオフにします。

     

**注**  上位プロトコルまたはフィルター ドライバーがすべての基になるミニポート ドライバーの設定にフィルターを受信パケットの結合をクリアする必要があります、バインドの解除を完了するか、操作をデタッチする前にします。

 

 

 





