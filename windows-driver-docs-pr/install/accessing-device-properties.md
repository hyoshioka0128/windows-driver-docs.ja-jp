---
title: デバイス プロパティへのアクセス
description: デバイス プロパティへのアクセス
ms.assetid: 7D3F3164-E530-49fb-BCCD-9C024543FA95
keywords:
- デバイスのプロパティへのアクセス、WDK デバイスのインストール
- デバイスの WDK デバイス インストールのプロパティにアクセスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3c6caf1dca07278044c356f1f1fd05285c71e9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574473"
---
# <a name="accessing-device-properties"></a>デバイス プロパティへのアクセス


検出または変更する必要がありますいない[デバイス プロパティ](device-properties.md)レジストリ キーに直接アクセスします。 レジストリ キーでは、必要な情報の検出またはデバイスのプロパティを変更するのには含まれません。 さらに、場所、形式、およびこれらのキーの意味は、Windows の異なるバージョン間で変更可能性があります。

[SetupAPI](setupapi.md)関数は、一貫した動作を提供し、デバイス プロパティを保護するアクセス許可を適用します。 Windows Vista 以降、書き込みアクセスが制限されているデバイスのプロパティもアクセスが制限読み取り。

デバイスのプロパティに安全にアクセスするには、次のガイドラインに従います。

-   ユーザー モード アプリケーションでは、次の手順に従います。

    1.  使用して、Windows Vista 以降、 [ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) 、デバイスのプロパティを取得して使用し[ **SetupDiSetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552163)DEVPKEY_Xxx プロパティのコードをデバイスのプロパティを設定するとします。

        Windows Vista および以降のバージョンの Windows デバイスのインスタンスのプロパティに関する詳細については、[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)を参照してください。

        **注**  以降 Windows Vista では、いくつかのデバイス プロパティは、オペレーティング システムによって予約されています。 詳細については、[デバイス プロパティの変更](modifying-device-properties.md)を参照してください。

    2.  Windows 2000、Windows XP、および Windows Server 2003 を使用して[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551122) 、デバイスのプロパティを取得して使用し[ **SetupDiSetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552169) SPDRP_Xxx プロパティのコードをデバイスのプロパティを設定するとします。

        Windows 2000、Windows XP、および Windows Server 2003 デバイス インスタンスのプロパティに関する詳細については、[デバイス インスタンス SPDRP_Xxx プロパティへのアクセス](accessing-device-instance-spdrp-xxx-properties.md)を参照してください。

    3.  物理的に存在するデバイスのカスタム設定といない方は、レジストリ内で永続的なストレージを使用します。 この場合は、独自のレジストリ キーと値のセットを作成する必要があります。 これを行うには、次のように使用します。 **SetupDiCreateDevRegKey** (DIREG_DEV) または*ソフトウェア キー* (DIREG_DRV) デバイス。

        **注**  デバイスがアンインストールされるまで、ハードウェア キーがレジストリに永続化します。 ソフトウェア キーを移動またはでオフになって、[デバイス インストール コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)ドライバーのアップグレード中に

        カスタムの設定を保存するには使用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)レジストリ キーが作成または開きます。

-   カーネル モード ドライバーでは、使用[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)デバイス プロパティにアクセスします。

 

 





