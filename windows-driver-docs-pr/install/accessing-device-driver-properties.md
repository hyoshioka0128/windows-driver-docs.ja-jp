---
title: デバイス ドライバーのプロパティへのアクセス
description: デバイス ドライバーのプロパティへのアクセス
ms.assetid: 433ad114-46aa-470b-b529-e6b6fb7f6bd7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1078a9fe4e6f69035f855fe0817f1f6e1e02eb97
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375709"
---
# <a name="accessing-device-driver-properties"></a>デバイス ドライバーのプロパティへのアクセス


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)デバイス ドライバーの特性を示すデバイス ドライバーのプロパティが含まれています。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 もこれらのデバイス ドライバーのプロパティのほとんどをサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、これらのバージョンの Windows では、次のメカニズムを使用して、表し、対応するプロパティの情報にアクセスします。

-   [対応するレジストリ エントリの値を持つデバイス ドライバーのプロパティにアクセスします。](#accessing-device-driver-properties-that-have-corresponding-registry-en)
-   [SetupDiGetDriverInstallParams を使用して、ドライバーのランクを取得するには](#using-setupdigetdriverinstallparams-to-retrieve-driver-rank)

以前のバージョンの Windows、Windows Vista およびそれ以降のバージョンとの互換性は維持するために、デバイス インターフェイスに関する情報にアクセスするこれら 2 つの方法もサポートします。 ただし、Windows Vista およびそれ以降のバージョンでこれらのプロパティにアクセスするのにプロパティのキーを使用する必要があります。

システム定義のデバイス ドライバーのプロパティの一覧は、次を参照してください。[デバイス ドライバーのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff541205)します。 デバイス ドライバーのプロパティは、Windows Vista およびそれ以降のバージョンのプロパティへのアクセスに使用するプロパティのキー識別子が表示されます。 プロパティのキーで提供される情報には、Windows Server 2003、Windows XP、および Windows 2000 のプロパティへのアクセスに使用できる対応するシステム定義のレジストリ エントリの値の名前が含まれます。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス ドライバーのプロパティにアクセスする方法については、次を参照してください。[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)します。

### <a href="" id="accessing-device-driver-properties-that-have-corresponding-registry-en"></a> 対応するレジストリ エントリの値を持つデバイス ドライバーのプロパティにアクセスします。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス ドライバーのプロパティにアクセスするには、次の手順を実行します。

1.  呼び出す[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)デバイス インスタンス用のソフトウェア キーへのハンドルを取得します。 次のパラメーター値を指定します。

    -   設定*DeviceInfoSet*にグローバル ソフトウェア キーを取得する対象のデバイス情報の要素が含まれるデバイス情報のセットを識別するハンドル。
    -   設定*DeviceInfoData*へのポインター、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)グローバル ソフトウェア キーを取得する対象のデバイス情報の要素を表す構造体です。
    -   設定*スコープ*DICS_FLAG_GLOBAL にします。
    -   設定*HwProfile*をゼロにします。
    -   設定*KeyType* DIREG_DRV にを構成します**SetupDiOpenDevRegKey**デバイス インスタンス用のソフトウェア キーへのハンドルを取得します。
    -   設定*samDesired* REGSAM に型指定されたの値で、このキーに必要なアクセスを指定します。 すべてのアクセスを設定*samDesired* KEY_ALL_ACCESS にします。

    場合に呼び出し[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)成功すると、 **SetupDiOpenDevRegKey**要求されたソフトウェア キーへのハンドルを返します。 関数呼び出しが失敗した場合、 **SetupDiOpenDevRegKey** INVALID_HANDLE_VALUE を返します。 後続の呼び出し[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

2.  呼び出しでハンドルを指定[RegQueryValueEx](https://go.microsoft.com/fwlink/p/?linkid=95398)または[RegSetValueEx](https://go.microsoft.com/fwlink/p/?linkid=95399)を取得またはデバイス インスタンス ドライバーのプロパティに対応するレジストリ エントリの値を設定します。

3.  呼び出す、 [RegCloseKey](https://go.microsoft.com/fwlink/p/?linkid=194543)キーへのアクセスは必要なくなりました後は、ソフトウェアのレジストリ キーを閉じます。

### <a href="" id="using-setupdigetdriverinstallparams-to-retrieve-driver-rank"></a> SetupDiGetDriverInstallParams を使用して、ドライバーのランクを取得するには

呼び出すことによって、デバイスの現在インストールされているドライバーのランクを取得するには、Windows Server 2003、Windows XP、および Windows 2000、 [ **SetupDiGetDriverInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff551978)します。 **SetupDiGetDriverInstallParams**へのポインターを取得、 [ **SP_DRVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553290)出力パラメーターでのドライバーを構造*DriverInstallParams*. **ランク**ドライバーのランクが取得された SP_DRVINSTALL_PARAMS 構造体のメンバーに含まれています。

 

 





