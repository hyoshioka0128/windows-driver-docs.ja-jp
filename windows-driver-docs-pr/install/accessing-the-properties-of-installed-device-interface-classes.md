---
title: インストール済みのデバイス インターフェイスのプロパティへのアクセス
description: インストール済みのデバイス インターフェイスのプロパティへのアクセス
ms.assetid: 4079DD59-878E-4b71-9815-543BA838C56D
keywords:
- デバイスインターフェイス WDK デバイスのインストール、プロパティへのアクセス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50fa39ca082a96f675f8155b622928c81aecc94a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841652"
---
# <a name="accessing-the-properties-of-installed-device-interfaces"></a>インストール済みのデバイス インターフェイスのプロパティへのアクセス


システムに登録されているデバイスインターフェイスの属性を検出するには、レジストリに直接アクセスして、デバイスインターフェイスサブキーを開いたり、読み取ったり、書き込んだりしないでください。 レジストリキーと同様に、キーの場所、名前、または形式は、Windows の異なるバージョン間で変更される可能性があります。

デバイスインターフェイスの属性を安全に照会および変更するには、次のガイドラインに従います。

-   ユーザーモードアプリケーションは、次の手順に従う必要があります。

    1.  [**Setupdiopendeviceinterface**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfacea)を使用してデバイスインターフェイスを検索し、そのインターフェイスを名前からセットに追加します。

    2.  [**Setupdigetdeviceinterfacedetail**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)を使用して、デバイスインターフェイスの詳細を取得します。

        オプションの*Deviceinfodata*パラメーターは、インターフェイスが登録されているデバイスの[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)要素を受け取ります。

    3.  デバイスインターフェイスクラスのカスタム設定には、永続的なレジストリストレージを使用します。 これを行うには、 [**SetupDiCreateDeviceInterfaceRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya) (新しいレジストリキーを作成する場合) または[**SetupDiOpenDeviceInterfaceRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey) (既存のレジストリキーを開く場合) を使用します。

        カスタム設定を保存するには、レジストリキーが作成または開かれた後に[Regclosekey](https://go.microsoft.com/fwlink/p/?linkid=194543)を使用します。

-   カーネルモードドライバーは、 [**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)を使用して、デバイスインターフェイスクラスのレジストリキーを開く必要があります。

 

 





