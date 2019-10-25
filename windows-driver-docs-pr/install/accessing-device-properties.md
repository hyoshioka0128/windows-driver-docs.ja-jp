---
title: デバイス プロパティへのアクセス
description: デバイス プロパティへのアクセス
ms.assetid: 7D3F3164-E530-49fb-BCCD-9C024543FA95
keywords:
- デバイスのプロパティ WDK デバイスのインストール、アクセス
- デバイスプロパティへのアクセス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab6ed86e947b47b2060802a33893709b037f926c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841654"
---
# <a name="accessing-device-properties"></a>デバイス プロパティへのアクセス


レジストリキーに直接アクセスすることによって、[デバイスのプロパティ](device-properties.md)を検出または変更することはできません。 レジストリキーには、デバイスのプロパティを検出または変更するために必要な情報は含まれていません。 また、これらのキーの場所、形式、および意味は、異なるバージョンの Windows で変更される可能性があります。

[Setupapi.log](setupapi.md)関数は一貫した動作を提供し、デバイスのプロパティを保護するアクセス許可を適用します。 Windows Vista 以降では、書き込みアクセスが制限されているデバイスプロパティにも読み取りアクセスが制限されています。

デバイスのプロパティに安全にアクセスするには、次のガイドラインに従ってください。

-   ユーザーモードアプリケーションの場合は、次の手順を実行します。

    1.  Windows Vista 以降では、 [**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)を使用してデバイスのプロパティを取得し、 [**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)と DEVPKEY_Xxx プロパティコードを使用してデバイスのプロパティを設定します。

        Windows Vista 以降のバージョンの Windows でのデバイスインスタンスのプロパティの詳細については、「[デバイスインスタンスのプロパティへのアクセス (Windows vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)」を参照してください。

        **注**  Windows Vista 以降では、一部のデバイスプロパティがオペレーティングシステムによって予約されています。 詳細については、「[デバイスプロパティの変更](modifying-device-properties.md)」を参照してください。

    2.  Windows 2000、Windows XP、および Windows Server 2003 では、 [**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)を使用してデバイスのプロパティを取得し、 [**SetupDiSetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)と SPDRP_Xxx プロパティコードを使用してデバイスのプロパティを設定します。

        Windows 2000、Windows XP、および Windows Server 2003 のデバイスインスタンスのプロパティの詳細については、「[デバイスインスタンスの SPDRP_Xxx プロパティへのアクセス](accessing-device-instance-spdrp-xxx-properties.md)」を参照してください。

    3.  物理的に存在するデバイスとそうでないデバイスのカスタム設定には、レジストリ内で永続ストレージを使用します。 この場合は、独自のレジストリキーと値のセットを作成する必要があります。 これを行うには、デバイスに**Setupdicreatedevregkey** (DIREG_DEV) または*ソフトウェアキー* (DIREG_DRV) を使用します。

        デバイスがアンインストールされるまで、ハードウェア**キー  レジストリ**に保持されます。 ソフトウェアキーは、ドライバーのアップグレード中に[デバイスのインストールコンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))によって移動またはクリアされます。

        カスタム設定を保存するには、レジストリキーが作成または開かれた後に[Regclosekey](https://go.microsoft.com/fwlink/p/?linkid=194543)を使用します。

-   カーネルモードドライバーの場合は、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)を使用して、デバイスのプロパティにアクセスします。

 

 





