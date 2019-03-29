---
title: インストール済みのデバイス インターフェイスのプロパティへのアクセス
description: インストール済みのデバイス インターフェイスのプロパティへのアクセス
ms.assetid: 4079DD59-878E-4b71-9815-543BA838C56D
keywords:
- デバイス インターフェイスのプロパティへのアクセス、WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ca0bc49279780ca2150d912a08bc7012e852c66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581720"
---
# <a name="accessing-the-properties-of-installed-device-interfaces"></a>インストール済みのデバイス インターフェイスのプロパティへのアクセス


システムに登録されているデバイスのインターフェイスの属性を検出するには、必要がありますいないを開く、読み書きする、デバイス インターフェイス サブキーによって直接レジストリへのアクセスします。 任意のレジストリ キーと同様、場所、名、またはキーの形式が Windows の異なるバージョン間変更可能性があります。

安全にクエリを実行して、デバイス インターフェイスの属性を変更するには、次のガイドラインを使用します。

-   ユーザー モード アプリケーションは、次の手順に従う必要があります。

    1.  使用[ **SetupDiOpenDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff552074)デバイス インターフェイスを見つけて、その名前から、セットに追加します。

    2.  使用[ **SetupDiGetDeviceInterfaceDetail** ](https://msdn.microsoft.com/library/windows/hardware/ff551120)デバイス インターフェイスの詳細を取得します。

        省略可能な*DeviceInfoData*パラメーターが表示されます、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)インターフェイスで登録されたデバイスの要素。

    3.  デバイスのインターフェイス クラスのカスタム設定のレジストリの永続的なストレージを使用します。 これを行うには、次のように使用します[ **SetupDiCreateDeviceInterfaceRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550967) (新しいレジストリ キーを作成) するまたは[ **SetupDiOpenDeviceInterfaceRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552075)。(を既存のレジストリ キーを開きます)。

        カスタムの設定を保存するには使用[RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)レジストリ キーが作成または開きます。

-   カーネル モード ドライバーを使用する必要があります[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)デバイス インターフェイス クラスのレジストリ キーを開けません。

 

 





