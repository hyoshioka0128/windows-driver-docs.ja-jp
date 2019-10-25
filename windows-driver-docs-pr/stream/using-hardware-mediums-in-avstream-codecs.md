---
title: AVStream コーデックでのハードウェアメディアの使用
description: AVStream コーデックでのハードウェアメディアの使用
ms.assetid: 07c25875-c549-4d47-ac0d-605f2aa9daa4
keywords:
- AVStream ハードウェアコーデックサポート WDK、ハードウェアメディアを使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcdfa1dab865d860c142a08fce7435519d1aa75e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842294"
---
# <a name="using-hardware-mediums-in-avstream-codecs"></a>AVStream コーデックでのハードウェアメディアの使用


プライベートメディアをサポートする AVStream ミニドライバーは、システムメモリへの中間転送を行わずに、デバイスハードウェアのデータを転送できます。

具体的には、2つのフィルターが同じプライベートメディアおよび中規模インスタンスを共有している場合、メディアファンデーションはデバイスハードウェアでメディアを排他的に転送します。 この転送は、関数がシステムメモリに取り込まれることなく行われます。 たとえば、同じデバイスのデコーダーとエンコーダーがプライベートメディアを共有でき、その結果、パフォーマンスが大幅に向上します。

プライベートメディアを使用するには、ミニドライバーがピンの[*Avstrminipinprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin)関数で次の操作を行う必要があります。

1.  Pin 接続に対してドライバーのカスタムメディアが選択されている場合 (pin の中に\_KSMEDIUMSETID が使用されていない場合など) は、そのプライベートバスを介してデータをルーティングする必要があります。 AVStream では、カスタムメディアを使用して接続されているピンのストリームポインタートランスポートが有効になりません。

2.  ドライバーは、 [**Kspingetconnectedpinfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetconnectedpinfileobject)を呼び出して、接続されている pin を特定できます。

3.  ドライバーは、バッファーに対して操作を実行し、カスタムメディアを介して接続されたピン/フィルターオブジェクトにルーティングできます。

 

 




