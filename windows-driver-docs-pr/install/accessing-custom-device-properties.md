---
title: カスタム デバイス プロパティへのアクセス
description: カスタム デバイス プロパティへのアクセス
ms.assetid: 81170fd5-f1fb-4a06-a651-4651fc894070
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed93a7ce014730a80c06b078104dbb1b87cd2e5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385632"
---
# <a name="accessing-custom-device-properties"></a>カスタム デバイス プロパティへのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)の使用をサポート[プロパティ キー](property-keys.md)を作成し、カスタムのデバイスのプロパティにアクセスします。 詳細については、次を参照してください。[カスタム デバイス プロパティの作成](creating-custom-device-properties.md)です。

Windows Server 2003、Windows XP、および Windows 2000 では、カスタム レジストリにデバイス関連のコンポーネントのシステム提供のレジストリ キーの下のエントリの値を作成できます。 次の一覧には、対応するシステム提供のレジストリ キーをデバイス コンポーネントの種類ごとに呼び出される SetupAPI 関数が含まれています。 システム定義のレジストリ キーを開くと、アプリケーションおよびインストーラーは、開いているレジストリ キーの下のカスタム レジストリ エントリの値を変更する Windows ベースのレジストリの関数を呼び出すことができます。

-   デバイス インスタンスのハードウェア プロパティのカスタム レジストリ エントリの値は、デバイスのインスタンスのハードウェアのレジストリ キーの下にあります。 呼び出す[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)で DIREG_DEV を指定し、*フラグ*デバイス インスタンスのハードウェア キーへのハンドルを取得するパラメーター。 デバイス インスタンスを呼び出すことによって取得できるため、ハードウェアのレジストリ キーの下に設定されているカスタム レジストリ エントリの値、 [ **SetupDiGetCustomDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetcustomdevicepropertya)関数。

-   デバイス インスタンス ソフトウェア プロパティのカスタム レジストリ エントリの値は、デバイスのインスタンスのソフトウェアのレジストリ キーの下にあります。 呼び出す**SetupDiOpenDevRegKey**で DIREG_DRV を指定し、*フラグ*デバイス インスタンスのソフトウェア キーへのハンドルを取得するパラメーター。

-   カスタム レジストリ エントリの値を[デバイス セットアップ クラス プロパティ](accessing-device-setup-class-properties.md)デバイス セットアップ クラスのレジストリ キーの下にあります。 呼び出す[ **SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)で DIOCR_INSTALLER を指定し、*フラグ*デバイス セットアップ クラスのレジストリ キーを識別するハンドルを取得するパラメーター。

-   デバイスのインターフェイス クラスのプロパティのカスタム レジストリ エントリの値は、デバイス インターフェイス クラスのレジストリ キーの下にあります。 呼び出す**SetupDiOpenClassRegKeyEx**で DIOCR_INTERFACE を指定し、*フラグ*デバイス インターフェイスのクラスのレジストリ キーを識別するハンドルを取得するパラメーター。

-   デバイスのインターフェイス プロパティのカスタム レジストリ エントリの値は、デバイス インターフェイスのレジストリ キーの下にあります。 呼び出す[ **SetupDiOpenDeviceInterfaceRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)デバイス インターフェイスのクラスのレジストリ キーを識別するハンドルを取得します。

レジストリ キーを識別するハンドルを取得した後に指定の呼び出しでハンドル[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)または[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)を取得またはカスタムのデバイスに対応するカスタム レジストリ エントリの値を設定するにはプロパティ。

呼び出す、 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)レジストリ キーへのアクセスは必要なくなりました後レジストリ キーを閉じます。

 

 





