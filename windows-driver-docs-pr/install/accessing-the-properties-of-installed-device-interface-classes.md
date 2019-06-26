---
title: インストール済みのデバイス インターフェイスのプロパティへのアクセス
description: インストール済みのデバイス インターフェイスのプロパティへのアクセス
ms.assetid: 4079DD59-878E-4b71-9815-543BA838C56D
keywords:
- デバイス インターフェイスのプロパティへのアクセス、WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b7e9aef5c01f0324e545a02b3acae84b0fed74d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386041"
---
# <a name="accessing-the-properties-of-installed-device-interfaces"></a>インストール済みのデバイス インターフェイスのプロパティへのアクセス


システムに登録されているデバイスのインターフェイスの属性を検出するには、必要がありますいないを開く、読み書きする、デバイス インターフェイス サブキーによって直接レジストリへのアクセスします。 任意のレジストリ キーと同様、場所、名、またはキーの形式が Windows の異なるバージョン間変更可能性があります。

安全にクエリを実行して、デバイス インターフェイスの属性を変更するには、次のガイドラインを使用します。

-   ユーザー モード アプリケーションは、次の手順に従う必要があります。

    1.  使用[ **SetupDiOpenDeviceInterface** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfacea)デバイス インターフェイスを見つけて、その名前から、セットに追加します。

    2.  使用[ **SetupDiGetDeviceInterfaceDetail** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)デバイス インターフェイスの詳細を取得します。

        省略可能な*DeviceInfoData*パラメーターが表示されます、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)インターフェイスで登録されたデバイスの要素。

    3.  デバイスのインターフェイス クラスのカスタム設定のレジストリの永続的なストレージを使用します。 これを行うには、次のように使用します[ **SetupDiCreateDeviceInterfaceRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya) (新しいレジストリ キーを作成) するまたは[ **SetupDiOpenDeviceInterfaceRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)。(を既存のレジストリ キーを開きます)。

        カスタムの設定を保存するには使用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)レジストリ キーが作成または開きます。

-   カーネル モード ドライバーを使用する必要があります[ **IoOpenDeviceInterfaceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)デバイス インターフェイス クラスのレジストリ キーを開けません。

 

 





