---
title: Windows Vista より前に、のデバイス インターフェイスのプロパティにアクセスします。
description: Windows Vista より前に、のデバイス インターフェイスのプロパティにアクセスします。
ms.assetid: 48b47d01-ec07-49ca-a03c-c4c387dcfb19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dcc5dead79529f0fe8dacc4e40fdc7a4e56516c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382927"
---
# <a name="accessing-device-interface-properties-before-windows-vista"></a>Windows Vista より前に、のデバイス インターフェイスのプロパティにアクセスします。


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)デバイス インターフェイスの特性を示すデバイス インターフェイスのプロパティが含まれています。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 は、これらのデバイス インターフェイス クラスのプロパティのほとんどをサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、これらのバージョンの Windows では、次のメカニズムを使用して、表し、デバイス インターフェイスのプロパティにアクセスします。

-   [対応するレジストリ エントリの値を持つデバイス インターフェイスのプロパティにアクセスします。](#accessing-device-interface-properties-that-have-corresponding-registry)

-   [SetupDiEnumDeviceInterfaces を使用して、デバイス インターフェイスに関する情報を取得する](#using-setupdienumdeviceinterfaces-to-retrieve-information-about-a-devi)します。

以前のバージョンの Windows、Windows Vista およびそれ以降のバージョンとの互換性は維持するために、デバイス インターフェイスに関する情報にアクセスするこれら 2 つの方法もサポートします。 ただし、Windows Vista およびそれ以降のバージョンでこれらのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

デバイスのシステム定義のインターフェイス クラスのプロパティの一覧は、次を参照してください。[デバイス インターフェイスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541409)します。 デバイスのインターフェイス クラスのプロパティは、Windows Vista およびそれ以降のバージョンのプロパティにアクセスするために使用に対応するキーのプロパティが表示されます。 プロパティのキーで提供される情報が含まれています、対応するレジストリ エントリの値には、存在する場合のプロパティを Windows Server 2003、Windows XP、および Windows 2000 へのアクセスに使用できます。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス セットアップ クラスのプロパティにアクセスする方法については、次を参照してください。[プロパティへのアクセス デバイス インターフェイス (Windows Vista 以降)](accessing-device-interface-properties--windows-vista-and-later-.md)します。

インストールして、デバイス インターフェイスを使用する方法については、次を参照してください。[デバイス インターフェイス クラス](device-interface-classes.md)と[ **INF AddInterface ディレクティブ**](inf-addinterface-directive.md)します。

### <a href="" id="accessing-device-interface-properties-that-have-corresponding-registry"></a> 対応するレジストリ エントリの値を持つデバイス インターフェイスのプロパティにアクセスします。

Windows Server 2003、Windows XP、および Windows 2000 では、最初の呼び出しでレジストリ エントリの値を使用して、デバイス インターフェイス プロパティにアクセスする[ **SetupDiOpenDeviceInterfaceRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552075)し、次を指定します。パラメーター:

-   設定*DeviceInfoSet*デバイス情報のセットを含む、デバイス インターフェイスへのポインター。

-   設定*DeviceInterfaceData*へのポインター、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)デバイス インターフェイスを識別する構造体。

-   設定*予約*をゼロにします。

-   設定*samDesired*必要なアクセス許可を指定する REGSAM に型指定された値にします。

この呼び出し場合[ **SetupDiOpenDeviceInterfaceRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552075)成功すると、 **SetupDiOpenDeviceInterfaceRegKey**要求ハンドルを返します。 関数呼び出しが失敗した場合、 **SetupDiOpenDeviceInterfaceRegKey** INVALID_HANDLE_VALUE とへの呼び出しを返します[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

デバイス インターフェイスのレジストリ キーを識別するハンドルを取得した後に指定の呼び出しでハンドル[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)または[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)を取得または設定に対応するレジストリ エントリの値、デバイス インターフェイスのプロパティです。

呼び出す、 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)キーへのアクセスは必要なくなりました後に、クラスのレジストリ キーを閉じます。

### <a href="" id="using-setupdienumdeviceinterfaces-to-retrieve-information-about-a-devi"></a> SetupDiEnumDeviceInterfaces を使用して、デバイス インターフェイスに関する情報を取得するには

Windows Server 2003、Windows XP、および Windows 2000 上のデバイス インターフェイスに関する情報を取得する別の方法は呼び出すことによって、 [ **SetupDiEnumDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff551015)を取得する、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)インターフェイスの構造体。 SP_DEVICE_INTERFACE_DATA 構造体には、次の情報が含まれています。

-   **フラグ**メンバーは、デバイス インターフェイスは、アクティブまたは、削除されたかどうかと、デバイスのインターフェイス クラスの既定のインターフェイスがかどうかを示します。

-   **InterfaceClassGuild**メンバが、インターフェイス クラス GUID によって識別されます。

 

 





