---
title: USBPRINT のプログラミング考慮事項
description: USBPRINT のプログラミング考慮事項
ms.assetid: 351b3124-d584-4817-a5ce-09e16b54d41b
keywords:
- プリンタードライバー WDK、USB
- USBPRINT
- USBMON
- USB プリンター WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a38d7f14d1f0a350809a98fb3d374e5242630b65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840426"
---
# <a name="programming-considerations-for-usbprint"></a>USBPRINT のプログラミング考慮事項





Usbprint は、USBPRINT と共に、並列プリンターで使用されるインターフェイスと非常によく似ています。 多くの場合、1つのプリンタードライバーまたは言語モニターが、変更なしで並列プリンターと USB プリンターの両方で正しく動作する可能性があります。 言語モニターが[**Writeport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)および[**readport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)関数だけを使用し、 [**IOCTL\_PAR\_クエリ\_デバイス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id)要求を使用している場合、USB とパラレルプリンターの間で移植性があります。

場合によっては、特殊なプリンター機能を利用するために、言語モニターがプリンターに対してベンダー固有の要求を行う必要があります。 これを行うには、 [**ioctl\_usbprint\_ベンダを使用し\_\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command)と[**IOCTL\_USBPRINT\_ベンダ\_GET\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)を設定します。 ただし、これらの Ioctl を使用すると、パラレルポートモニターと互換性のない言語モニターがレンダリングされます。

通常、言語モニターは、管理しているプリンターのデバイスハンドルにアクセスできません。 代わりに、言語モニターとバスドライバー (この場合は Usbprint. sys) の間にあるポートモニターによって提供されるポート名を持ちます。 詳細については[、「言語およびポートモニターの相互作用](language-and-port-monitor-interaction.md)」を参照してください。 デバイスハンドルがないため、言語モニターはデバイスバスドライバーの Ioctl を直接呼び出すことができません。 この制限を克服するために、USBMON は[**GetPrinterDataFromPort**](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85)) API を実装しています。これにより、言語モニターは USBMON から usbmon によって ioctl を発行できます。

USB 印刷スタックは、次の Api と IOCTL を並列印刷スタックと共有します。

[**WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)

[**ReadPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)

[**IOCTL\_PAR\_クエリ\_デバイス\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id)

次の Ioctl は、USB 印刷スタックに固有です。

[**IOCTL\_USBPRINT\_GET\_1284\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_1284_id)

[**IOCTL\_USBPRINT\_\_LPT\_の状態を取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_get_lpt_status)

[**IOCTL\_USBPRINT\_ソフト\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_soft_reset)

[**IOCTL\_USBPRINT\_ベンダ\_\_コマンドを取得します。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_get_command)

[**IOCTL\_USBPRINT\_ベンダ\_SET\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbprint/ni-usbprint-ioctl_usbprint_vendor_set_command)

**  ** usbprint は、デバイスから記述子を取得するためのメカニズムや、直接 USB パイプを操作する機構を提供しません。

 

 

 




