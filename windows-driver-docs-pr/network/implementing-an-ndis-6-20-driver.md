---
title: NDIS 6.20 ドライバーの実装
description: NDIS 6.20 ドライバーの実装
ms.assetid: 6c6f83ff-2a6f-4e5d-acc0-70835429312d
keywords:
- NDIS 6.20 WDK、ドライバーを実装します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c911117c3c51f89408cfc357e960b78711a564f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383626"
---
# <a name="implementing-an-ndis-620-driver"></a>NDIS 6.20 ドライバーの実装





NDIS 6.20 が動作ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。

NDIS のメジャーおよびマイナー NDIS バージョン番号を更新する必要があります\_*Xxx*\_ドライバー\_NDIS 6.20 が動作をサポートする特性構造体。 **MajorNdisVersion**メンバーは、6 を含める必要があります、 **MinorNdisVersion**メンバーは、20 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 バージョン情報を更新することも必要があります。 コンパイラは、次を参照してください。 [NDIS 6.20 ドライバーをコンパイルする](compiling-an-ndis-6-20-driver.md)します。

NDIS 6.20 電源の管理サービスは、NDIS 6.20 が動作し、それ以降のミニポート ドライバーでは必須です。 NDIS 6.20 電源管理のインターフェイスの詳細については、次を参照してください。 [NDIS 6.20 で電源管理の機能強化](power-management-enhancements-in-ndis-6-20.md)します。

NDIS direct OID 要求インターフェイスは、NDIS 6.20 が動作し、それ以降のミニポート ドライバーに必須です。 Oid の直接のインターフェイスの詳細については、次を参照してください。 [Direct OID 要求インターフェイスで NDIS 6.1](direct-oid-request-interface-in-ndis-6-1.md)します。

NDIS とデバイスの上にあるドライバーとドライバーを通知するためには、機能、NDIS 6.20 が動作およびそれ以降のドライバーが次の機能の NDIS 6.20 が動作のデバイス機能インターフェイスを実装する必要があります。

-   [電源管理](power-management-enhancements-in-ndis-6-20.md)

-   [Receive Side Scaling (RSS)](ndis-receive-side-scaling2.md)

-   [仮想マシン キュー (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)

NDIS 6.20 が動作し、後でドライバーをサポートする必要があります受信側のスロットル (RST) は、割り込みを受信します。 RST の詳細については、次を参照してください。[受信側スロットル NDIS 6.20](receive-side-throttle-in-ndis-6-20.md)します。

NDIS 6.20 対応と古い形式のインターフェイスを使用するコードに置き換えます。 廃止された関数の詳細については、次を参照してください。 [NDIS 6.20 で古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)します。 NDIS 6.20 が動作バージョンをサポートする構造を更新する方法の詳細については、次を参照してください。 [NDIS 6.20 データ構造体を使用して](using-ndis-6-20-data-structures.md)します。

64 を超えるプロセッサをサポートして、たとえば、NDIS 6.20 読み取りを使用し、ロックのインターフェイスを作成するための NDIS インターフェイスを使用します。 64 を超えるプロセッサのサポートの詳細については、次を参照してください。[を NDIS 6.20 で 64 を超えるプロセッサのサポート](support-for-more-than-64-processors-in-ndis-6-20.md)します。

 

 





