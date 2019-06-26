---
title: デバイス プロパティへのアクセス
description: デバイス プロパティへのアクセス
ms.assetid: 7D3F3164-E530-49fb-BCCD-9C024543FA95
keywords:
- デバイスのプロパティへのアクセス、WDK デバイスのインストール
- デバイスの WDK デバイス インストールのプロパティにアクセスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 309e9583b3880040798ace2ea43d7bd10e4b5893
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385018"
---
# <a name="accessing-device-properties"></a>デバイス プロパティへのアクセス


検出または変更する必要がありますいない[デバイス プロパティ](device-properties.md)レジストリ キーに直接アクセスします。 レジストリ キーでは、必要な情報の検出またはデバイスのプロパティを変更するのには含まれません。 さらに、場所、形式、およびこれらのキーの意味は、Windows の異なるバージョン間で変更可能性があります。

[SetupAPI](setupapi.md)関数は、一貫した動作を提供し、デバイス プロパティを保護するアクセス許可を適用します。 Windows Vista 以降、書き込みアクセスが制限されているデバイスのプロパティもアクセスが制限読み取り。

デバイスのプロパティに安全にアクセスするには、次のガイドラインに従います。

-   ユーザー モード アプリケーションでは、次の手順に従います。

    1.  使用して、Windows Vista 以降、 [ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 、デバイスのプロパティを取得して使用し[ **SetupDiSetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)DEVPKEY_Xxx プロパティのコードをデバイスのプロパティを設定するとします。

        Windows Vista および以降のバージョンの Windows デバイスのインスタンスのプロパティに関する詳細については、次を参照してください。[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)します。

        **注**  以降 Windows Vista では、いくつかのデバイス プロパティは、オペレーティング システムによって予約されています。 詳細については、次を参照してください。[デバイス プロパティの変更](modifying-device-properties.md)します。

    2.  Windows 2000、Windows XP、および Windows Server 2003 を使用して[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw) 、デバイスのプロパティを取得して使用し[ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya) SPDRP_Xxx プロパティのコードをデバイスのプロパティを設定するとします。

        Windows 2000、Windows XP、および Windows Server 2003 デバイス インスタンスのプロパティに関する詳細については、次を参照してください。[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](accessing-device-instance-spdrp-xxx-properties.md)します。

    3.  物理的に存在するデバイスのカスタム設定といない方は、レジストリ内で永続的なストレージを使用します。 この場合は、独自のレジストリ キーと値のセットを作成する必要があります。 これを行うには、次のように使用します。 **SetupDiCreateDevRegKey** (DIREG_DEV) または*ソフトウェア キー* (DIREG_DRV) デバイス。

        **注**  デバイスがアンインストールされるまで、ハードウェア キーがレジストリに永続化します。 ソフトウェア キーを移動またはでオフになって、[デバイス インストール コンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))ドライバーのアップグレード中に

        カスタムの設定を保存するには使用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)レジストリ キーが作成または開きます。

-   カーネル モード ドライバーでは、使用[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)デバイス プロパティにアクセスします。

 

 





