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
ms.openlocfilehash: 53b4b909a861d9b57a95ead21fce0d001ebb3d39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356023"
---
# <a name="programming-considerations-for-usbprint"></a>USBPRINT のプログラミング考慮事項





USBMON、と共に、Usbprint.sys では、並列のプリンターで使用するには非常に似たインターフェイスを提供します。 多くの場合は、並列と変更を加えなければ USB プリンターの両方で正常に動作する 1 つのプリンター ドライバーや言語モニター可能性があります。 言語モニターがのみで使用する場合、 [ **WritePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-writeport)と[**して**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-readport)関数と[ **IOCTL\_PAR\_クエリ\_デバイス\_ID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_device_id)要求、USB およびパラレル プリンターの間で移植可能になります。

場合によっては、言語モニターをプリンター特別なプリンターの機能を活用するためにベンダー固有の要求を行うために必要な場合があります。 これを行うには、次のように使用します[ **IOCTL\_USBPRINT\_ベンダー\_設定\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command)と[ **IOCTL\_ 。USBPRINT\_ベンダー\_取得\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)します。 ただし、これらの Ioctl を使用することを言語モニター レンダリング パラレル ポート モニターと互換性がありません。

通常、言語モニターには、プリンターを管理しているデバイス ハンドルへのアクセスはありません。 代わりに、言語モニターと、バス ドライバー (このケースで Usbprint.sys) の間でポート モニターによって提供されるポート名があります。 参照してください[言語およびポート モニターの相互作用](language-and-port-monitor-interaction.md)詳細についてはします。 デバイス ハンドルの不足は、言語モニターがデバイス バス ドライバーの Ioctl を直接呼び出すことを防ぎます。 USBMON を実装してこの制限を克服するために、 [ **GetPrinterDataFromPort** ](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85)) API により、言語モニターを USBPRINT USBMON を通じて Ioctl を発行します。

USB の印刷スタックは、並列の印刷スタックで、次の Api と IOCTL を共有します。

[**WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-writeport)

[**ReadPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-readport)

[**IOCTL\_PAR\_クエリ\_デバイス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_query_device_id)

次の Ioctl には、USB の印刷スタックに固有です。

[**IOCTL\_USBPRINT\_GET\_1284\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_1284_id)

[**IOCTL\_USBPRINT\_GET\_LPT\_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_get_lpt_status)

[**IOCTL\_USBPRINT\_ソフト\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_soft_reset)

[**IOCTL\_USBPRINT\_ベンダー\_取得\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)

[**IOCTL\_USBPRINT\_ベンダー\_設定\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command)

**注**   Usbprint.sys はも USB パイプを直接操作するため、デバイスからの記述子を取得するためのメカニズムを提供していません。

 

 

 




