---
title: デバイス インターフェイスのクラス プロパティにアクセスします。
description: デバイス インターフェイスのクラス プロパティにアクセスします。
ms.assetid: c9efe273-dc66-4585-8ab5-3842df1c95df
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4be0d5781dd6bc6e41865396f8a4d53815db0055
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551021"
---
# <a name="accessing-device-interface-class-properties"></a>デバイス インターフェイスのクラス プロパティにアクセスします。


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)デバイス インターフェイスのクラスの特性を示すデバイス インターフェイス クラスのプロパティが含まれています。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 もこれらのデバイス インターフェイス クラスのプロパティのほとんどをサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、表現し、次のメソッドを使用してこれらのバージョンの Windows に対応するプロパティの情報にアクセスできます。

-   [デバイスのインターフェイス クラスの既定のインターフェイスにアクセスします。](#accessing-the-default-interface-for-a-device-interface-class)

-   [インターフェイス クラスのレジストリ キーの下のレジストリ エントリの値を持つデバイス インターフェイスのクラス プロパティにアクセスします。](#accessing-device-interface-class-properties-that-have-registry-entry-v)

以前のバージョンの Windows、Windows Vista およびそれ以降のバージョンとの互換性は維持するために、デバイス インターフェイスに関する情報にアクセスするこれら 2 つの方法もサポートします。 ただし、Windows Vista およびそれ以降のバージョンでこれらのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

デバイスのシステム定義のインターフェイス クラスのプロパティの一覧は、次を参照してください。[デバイス インターフェイスのクラス プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541406)します。 [デバイス セットアップ クラスのプロパティ](accessing-device-setup-class-properties.md)Windows Vista およびそれ以降のバージョンのプロパティへのアクセスに使用するプロパティのキー識別子ごとに表示されます。 プロパティのキーで提供される情報には、Windows Server 2003、Windows XP、および Windows 2000 のプロパティへのアクセスに使用できる対応するレジストリ エントリの値も含まれています。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス セットアップ クラスのプロパティにアクセスする方法については、次を参照してください。[にアクセスするデバイス クラスのプロパティ (Windows Vista 以降)](accessing-device-class-properties--windows-vista-and-later-.md)します。

### <a href="" id="accessing-the-default-interface-for-a-device-interface-class"></a> デバイスのインターフェイス クラスの既定のインターフェイスにアクセスします。

デバイスのインターフェイス クラスの既定のインターフェイスを取得する[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)し、次のパラメーター値を指定します。

-   設定*ClassGuid*を既定のインターフェイスを取得する対象のデバイスのインターフェイス クラスを表す GUID。

-   設定 * 列挙子 ***NULL**します。

-   設定*hwndParent*に**NULL**します。

-   設定*フラグ*に (DIGCF_DEVICEINTERFACE |DIGCF_DEFAULT)。

この呼び出しでは、デバイス情報の要素が含まれるデバイス情報のセットを返します。 返されるデバイス情報要素は、指定したデバイスのインターフェイス クラスの既定のインターフェイスをサポートするデバイスを表します。

デバイス インターフェイスのクラスの既定のインターフェイスを設定するには、呼び出す[ **SetupDiSetDeviceInterfaceDefault** ](https://msdn.microsoft.com/library/windows/hardware/ff552149)し、次のパラメーター値を指定します。

-   設定*DeviceInfoSet*デバイス インターフェイスのクラスの既定として設定するデバイスのインターフェイスが含まれるデバイス情報のセットへのハンドル。

-   設定*DeviceInterfaceData*へのポインター、 [ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)でデバイスのインターフェイスを指定する構造体*DeviceInfoSet*.

### <a href="" id="accessing-device-interface-class-properties-that-have-registry-entry-v"></a> インターフェイス クラスのレジストリ キーの下のレジストリ エントリの値を持つデバイス インターフェイスのクラス プロパティにアクセスします。

インターフェイス クラスのレジストリ キーの下の対応するレジストリ エントリ値を持つデバイスのインターフェイス クラスのプロパティにアクセスするには、次の手順を実行します。

1.  呼び出す、 [ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)インターフェイス クラスのレジストリ キーを開き、次のパラメーター値を指定する関数。

    -   設定*ClassGuid*要求クラスのレジストリ キーのデバイスのインターフェイス クラスを識別する GUID へのポインター。
    -   設定*samDesired*必要なアクセス権限を示す REGSAM に型指定された値にします。
    -   設定*フラグ*DIOCR_INTERFACE にします。
    -   設定*MachineName*要求クラスのレジストリ キーを開くときにコンピューターの名前を含む NULL で終わる文字列へのポインター。 コンピューターがローカル コンピューターの場合は、設定*MachineName*に**NULL**します。
    -   設定*予約*に**NULL**します。

    この呼び出し場合[ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)成功すると、 **SetupDiOpenClassRegKeyEx**要求ハンドルを返します。 関数呼び出しが失敗した場合、 **SetupDiOpenClassRegKeyEx** INVALID_HANDLE_VALUE とへの呼び出しを返します[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)はログに記録されたエラー コードを返します。

2.  呼び出しで取得したハンドルを指定[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)と[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)を取得またはデバイスのインターフェイス クラス プロパティに対応するレジストリ エントリの値を設定します。

3.  呼び出す、 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)キーへのアクセスは必要なくなりました後に、クラスのレジストリ キーを閉じます。

インストールして、デバイス インターフェイスを使用する方法については、次を参照してください。[デバイス インターフェイス クラス](device-interface-classes.md)と[ **INF AddInterface ディレクティブ**](inf-addinterface-directive.md)します。

 

 





