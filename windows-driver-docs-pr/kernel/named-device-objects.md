---
title: 名前付きデバイス オブジェクト
description: 名前付きデバイス オブジェクト
ms.assetid: 4e24f0c1-57b2-4e06-a7f5-9a93d365ac8c
keywords:
- デバイスオブジェクト WDK カーネル、
- 名前付きデバイスオブジェクト WDK カーネル
ms.date: 09/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2c0f12483cb28a6b99187bbde8e0ebe8d68898b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838540"
---
# <a name="named-device-objects"></a>名前付きデバイス オブジェクト





すべてのオブジェクトマネージャーオブジェクトと同様に、デバイスオブジェクトに名前を付けたり名前を付けたりすることはできません。 ユーザーモードアプリケーションは i/o 要求を行うときに、名前によって操作のターゲットを指定します。 オブジェクトマネージャーは、名前を解決して i/o 要求の送信先を決定します。

> [!IMPORTANT]
> 必要な場合にのみ、ドライバーのセキュリティ名のデバイスオブジェクトを増やすことができます。 名前付きデバイスオブジェクトは、一般に、特定の名前を使用してデバイスを開くことが想定されているアプリケーションや、PNP 以外のデバイス/コントロールデバイスを使用している場合など、従来の理由でのみ必要になります。  WDF ドライバーは、 [WdfDeviceCreateSymbolicLink](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)を使用してシンボリックリンクを作成するために、PnP デバイスの名前を指定する必要がないことに注意してください。

ドライバーは、デバイスオブジェクトを作成するために[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)または[**iocreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)を呼び出すときに、デバイスオブジェクトの名前を指定できます。 デバイスオブジェクトに名前を指定するタイミングと方法の詳細については、「 [NT デバイス名](nt-device-names.md)」を参照してください。
  
名前付きデバイスオブジェクトには MS-DOS デバイス名を指定することもできます。これは、 [**IoIoCreateUnprotectedSymbolicLink Ymの Iclink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)または[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink)によって作成されたシンボリックリンクです。 WDM ドライバーは、一般に MS-DOS デバイス名を必要としません。 詳細については、「 [MS-DOS デバイス名](ms-dos-device-names.md)」を参照してください。

> [!IMPORTANT]
> 名前付きデバイスオブジェクトを使用する場合は、 [Iocreateデバイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)を使用して、セキュリティで保護できるように SDDL を指定することができます。 [IocreateDeviceClassGuid](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)を実装するときは、常にカスタムクラス GUID を指定します。 ここでは、既存のクラス GUID を指定しないでください。 これにより、そのクラスに属する他のデバイスのセキュリティ設定または互換性が損なわれる可能性があります。 詳細については、「 [WdmlibIoCreateDeviceSecure](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)」を参照してください。
> 
> アプリケーションまたはその他の WDF ドライバーが PnP デバイスにアクセスできるようにするには、デバイスインターフェイスを使用する必要があります。 詳細については、「[デバイスインターフェイスの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)」を参照してください。 デバイスインターフェイスは、デバイススタックの PDO へのシンボリックリンクとして機能します。 PDO へのアクセスを制御する方法としては、INF に SDDL 文字列を指定します。 SDDL 文字列が INF ファイルにない場合は、Windows によって既定のセキュリティ記述子が適用されます。 詳細については、「デバイスオブジェクトの[セキュリティ保護](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)」と「[デバイスオブジェクトの SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)」を参照してください。


このセクションには、次のサブセクションが含まれています。

[NT デバイス名](nt-device-names.md)

[MS-DOS デバイス名](ms-dos-device-names.md)

 

 




