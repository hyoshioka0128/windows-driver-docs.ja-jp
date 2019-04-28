---
title: USBPRINT のプログラミング考慮事項
description: USBPRINT のプログラミング考慮事項
ms.assetid: 351b3124-d584-4817-a5ce-09e16b54d41b
keywords:
- プリンター ドライバー WDK、USB
- USBPRINT
- USBMON
- WDK の USB プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f9b8b486cdcdf913c02f57dc683c2486efd158b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376578"
---
# <a name="programming-considerations-for-usbprint"></a>USBPRINT のプログラミング考慮事項





USBMON、と共に、Usbprint.sys では、並列のプリンターで使用するには非常に似たインターフェイスを提供します。 多くの場合は、並列と変更を加えなければ USB プリンターの両方で正常に動作する 1 つのプリンター ドライバーや言語モニター可能性があります。 言語モニターがのみで使用する場合、 [ **WritePort** ](https://msdn.microsoft.com/library/windows/hardware/ff563792)と[**して**](https://msdn.microsoft.com/library/windows/hardware/ff561909)関数と[ **IOCTL\_PAR\_クエリ\_デバイス\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff544076)要求、USB およびパラレル プリンターの間で移植可能になります。

場合によっては、言語モニターをプリンター特別なプリンターの機能を活用するためにベンダー固有の要求を行うために必要な場合があります。 これを行うには、次のように使用します[ **IOCTL\_USBPRINT\_ベンダー\_設定\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff551817)と[ **IOCTL\_ 。USBPRINT\_ベンダー\_取得\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff551815)します。 ただし、これらの Ioctl を使用することを言語モニター レンダリング パラレル ポート モニターと互換性がありません。

通常、言語モニターには、プリンターを管理しているデバイス ハンドルへのアクセスはありません。 代わりに、言語モニターと、バス ドライバー (このケースで Usbprint.sys) の間でポート モニターによって提供されるポート名があります。 参照してください[言語およびポート モニターの相互作用](language-and-port-monitor-interaction.md)詳細についてはします。 デバイス ハンドルの不足は、言語モニターがデバイス バス ドライバーの Ioctl を直接呼び出すことを防ぎます。 USBMON を実装してこの制限を克服するために、 [ **GetPrinterDataFromPort** ](https://msdn.microsoft.com/library/windows/hardware/ff550506) API により、言語モニターを USBPRINT USBMON を通じて Ioctl を発行します。

USB の印刷スタックは、並列の印刷スタックで、次の Api と IOCTL を共有します。

[**WritePort**](https://msdn.microsoft.com/library/windows/hardware/ff563792)

[**ReadPort**](https://msdn.microsoft.com/library/windows/hardware/ff561909)

[**IOCTL\_PAR\_クエリ\_デバイス\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff544076)

次の Ioctl には、USB の印刷スタックに固有です。

[**IOCTL\_USBPRINT\_GET\_1284\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551803)

[**IOCTL\_USBPRINT\_GET\_LPT\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/ff551809)

[**IOCTL\_USBPRINT\_ソフト\_リセット**](https://msdn.microsoft.com/library/windows/hardware/ff551810)

[**IOCTL\_USBPRINT\_ベンダー\_取得\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff551815)

[**IOCTL\_USBPRINT\_ベンダー\_設定\_コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff551817)

**注**   Usbprint.sys はも USB パイプを直接操作するため、デバイスからの記述子を取得するためのメカニズムを提供していません。

 

 

 




