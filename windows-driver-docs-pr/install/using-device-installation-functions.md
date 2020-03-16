---
title: デバイス インストール関数の使用
description: デバイス インストール関数の使用
ms.assetid: a7cfa359-a45c-45fa-a854-ee70de66b12e
keywords:
- Setupapi.log functions WDK、デバイスインストール関数
- デバイスのインストール機能 WDK Setupapi.log
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8201aacada4f2f5d09d6665f4167c20750d91d1
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242991"
---
# <a name="using-device-installation-functions"></a>デバイス インストール関数の使用





このセクションでは、[デバイスのインストール機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))について概要を説明します。 インストールソフトウェアは、デバイスのインストール機能を使用して、次の種類の操作を実行できます。

-   ドライバーのインストール

-   差分コードを処理します。

-   デバイス情報セットを管理します。

-   ドライバーの一覧を管理します。

-   デバイスインターフェイスを管理します。

-   アイコンとその他のビットマップを管理します。

このセクションで説明する Setupapi.log 機能でサポートされていないデバイスのインストール操作を実行するには、適切な[一般的なセットアップ関数](https://docs.microsoft.com/previous-versions/ff544985(v=vs.85))または[PnP Configuration Manager 関数](https://docs.microsoft.com/previous-versions/ff549717(v=vs.85))(CM_*Xxx*関数) を呼び出し<em>ます。</em>

次の表は、次の種類の関数の概要を示しています。

[ドライバーのインストール機能](#ddk-update-driver-function-dg)

[デバイス情報関数](#ddk-setupdi-device-information-functions-dg)

[ドライバー情報機能](#ddk-setupdi-driver-information-functions-dg)

[ドライバー選択機能](#ddk-setupdi-driver-selection-functions-dg)

[デバイスのインストールハンドラー](#ddk-setupdi-device-installation-handlers-dg)

[デバイスのインストールのカスタマイズ機能](#ddk-setupdi-device-installation-customization-functions-dg)

[セットアップクラスの関数](#ddk-setupdi-setup-class-functions-dg)

[ビットマップおよびアイコンの関数](#ddk-setupdi-class-bitmap-and-icon-functions-dg)

[デバイスインターフェイス関数](#ddk-setupdi-device-interface-functions-dg)

[デバイスプロパティ関数 (Windows Vista 以降)](#ddk-setupdi-device-property-functions-dg)

[レジストリ関数](#ddk-setupdi-registry-functions-dg)

[その他の関数](#ddk-other-setupdi-functions-dg)

### <a href="" id="ddk-update-driver-function-dg"></a>ドライバーのインストール機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice" data-raw-source="[&lt;strong&gt;DiInstallDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldevice)"><strong>DiInstallDevice</strong></a></p></td>
<td align="left"><p>システム内に存在する PnP デバイス上の<a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">ドライバーストア</a>にプレインストールされている、指定したドライバーをインストールします。 (Windows Vista 以降のバージョンの Windows)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera" data-raw-source="[&lt;strong&gt;DiInstallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diinstalldrivera)"><strong>DiInstallDriver</strong></a></p></td>
<td align="left"><p>ドライバーストアにドライバーをプレインストールし、システムに存在する一致する PnP デバイスにドライバーをインストールします。 (Windows Vista 以降のバージョンの Windows)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-dirollbackdriver" data-raw-source="[&lt;strong&gt;DiRollbackDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-dirollbackdriver)"><strong>DiRollbackDriver</strong></a></p></td>
<td align="left"><p>指定されたデバイスにインストールされているドライバーを、デバイスのバックアップドライバーセットにロールバックします。 (Windows Vista 以降のバージョンの Windows)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-dishowupdatedevice" data-raw-source="[&lt;strong&gt;DiShowUpdateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-dishowupdatedevice)"><strong>DiShowUpdateDevice</strong></a></p></td>
<td align="left"><p>指定したデバイスのハードウェアの更新ウィザードを表示します。 (Windows Vista 以降のバージョンの Windows)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diuninstalldevice" data-raw-source="[&lt;strong&gt;DiUninstallDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-diuninstalldevice)"><strong>DiUninstallDevice</strong></a></p></td>
<td align="left"><p>デバイスをアンインストールし、そのデバイスノード (<a href="https://docs.microsoft.com/windows-hardware/drivers/#wdkgloss-devnode" data-raw-source="&lt;em&gt;devnode&lt;/em&gt;"><em>devnode</em></a>) をシステムから削除します。 (Windows 7 以降のバージョンの Windows)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/installselecteddriver" data-raw-source="[&lt;strong&gt;InstallSelectedDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/installselecteddriver)"><strong>InstallSelectedDriver</strong></a></p></td>
<td align="left"><p>選択したデバイスに選択したドライバーをインストールします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa" data-raw-source="[&lt;strong&gt;UpdateDriverForPlugAndPlayDevices&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/newdev/nf-newdev-updatedriverforplugandplaydevicesa)"><strong>UpdateDriverForPlugAndPlayDevices</strong></a></p></td>
<td align="left"><p>システム内に存在する一致する PnP デバイス用にインストールされている関数ドライバーを更新します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-information-functions-dg"></a>デバイス情報関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist)"><strong>Setupdicreatedevice In、</strong></a></p></td>
<td align="left"><p>空の<a href="device-information-sets.md" data-raw-source="[device information set](device-information-sets.md)">デバイス情報セット</a>を作成します。 このセットは、クラス GUID に関連付けることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolistexa" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoListEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolistexa)"><strong>Setupdicreatedeviceinの Istex</strong></a></p></td>
<td align="left"><p>空のデバイス情報セットを作成します。 このセットは、クラス GUID に関連付けることができ、リモートコンピューター上のデバイス用にすることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)"><strong>SetupDiCreateDeviceInfo</strong></a></p></td>
<td align="left"><p>新しいデバイス情報要素を作成し、指定したデバイス情報セットに新しいメンバーとして追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)"><strong>SetupDiOpenDeviceInfo</strong></a></p></td>
<td align="left"><p>既存のデバイスインスタンスに関する情報を取得し、指定したデバイス情報セットに追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)"><strong>SetupDiEnumDeviceInfo</strong></a></p></td>
<td align="left"><p>デバイス情報セットのデバイス情報要素のコンテキスト構造体を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstanceId&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstanceida)"><strong>SetupDiGetDeviceInstanceId</strong></a></p></td>
<td align="left"><p>デバイス情報要素に関連付けられているデバイスインスタンス ID を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistclass" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListClass&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistclass)"><strong>SetupDiGetDeviceInfoListClass</strong></a></p></td>
<td align="left"><p>関連付けられたクラスがある場合に、デバイス情報セットに関連付けられているクラス GUID を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistdetaila" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListDetail&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinfolistdetaila)"><strong>Setupdigetdeviceindisks Istdetail</strong></a></p></td>
<td align="left"><p>クラス GUID、リモートコンピューターハンドル、リモートコンピューター名など、デバイス情報セットに関連付けられている情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevpropertysheetsa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevPropertySheets&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevpropertysheetsa)"><strong>SetupDiGetClassDevPropertySheets</strong></a></p></td>
<td align="left"><p>指定されたデバイス情報要素のプロパティシート、または指定されたデバイス情報セットの<a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">デバイスセットアップクラス</a>のハンドルを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>指定されたクラスのすべてのデバイスを含むデバイス情報セットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>ローカルコンピューターまたはリモートコンピューター上の指定されたクラスのすべてのデバイスを含むデバイス情報セットを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddevice" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddevice)"><strong>SetupDiSetSelectedDevice</strong></a></p></td>
<td align="left"><p>指定されたデバイス情報要素を、デバイス情報セットの現在選択されているメンバーとして設定します。 通常、この関数は、インストールウィザードによって使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddevice" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddevice)"><strong>SetupDiGetSelectedDevice</strong></a></p></td>
<td align="left"><p>指定されたデバイス情報セットについて、現在選択されているデバイスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>新しく作成されたデバイスインスタンスをプラグアンドプレイマネージャーに登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinfo)"><strong>SetupDiDeleteDeviceInfo</strong></a></p></td>
<td align="left"><p>指定されたデバイス情報セットからメンバーを削除します。 この関数では、実際のデバイスは削除されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist" data-raw-source="[&lt;strong&gt;SetupDiDestroyDeviceInfoList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydeviceinfolist)"><strong>SetupDiDestroyDeviceInfoList</strong></a></p></td>
<td align="left"><p>デバイス情報セットを破棄し、関連付けられているすべてのメモリを解放します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-driver-information-functions-dg"></a>ドライバー情報機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist" data-raw-source="[&lt;strong&gt;SetupDiBuildDriverInfoList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)"><strong>SetupDiBuildDriverInfoList</strong></a></p></td>
<td align="left"><p>指定されたデバイスインスタンスに関連付けられているドライバーの一覧、またはデバイス情報セットのグローバルクラスドライバーリストを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa" data-raw-source="[&lt;strong&gt;SetupDiEnumDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)"><strong>SetupDiEnumDriverInfo</strong></a></p></td>
<td align="left"><p>ドライバー情報リストのメンバーを列挙します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInfoDetail&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinfodetaila)"><strong>SetupDiGetDriverInfoDetail</strong></a></p></td>
<td align="left"><p>指定したドライバー情報要素の詳細情報を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)"><strong>SetupDiSetSelectedDriver</strong></a></p></td>
<td align="left"><p>ドライバーリストの指定されたメンバーを現在選択されているドライバーとして設定します。 現在選択されているドライバーがないように、ドライバーの一覧をリセットするために使用することもできます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddrivera" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetselecteddrivera)"><strong>SetupDiGetSelectedDriver</strong></a></p></td>
<td align="left"><p>インストールするドライバーとして選択されたドライバーリストのメンバーを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicanceldriverinfosearch" data-raw-source="[&lt;strong&gt;SetupDiCancelDriverInfoSearch&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicanceldriverinfosearch)"><strong>Setupdicの Eldriverinfosearch</strong></a></p></td>
<td align="left"><p>別のスレッドで現在進行中のドライバーリスト検索をキャンセルします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydriverinfolist" data-raw-source="[&lt;strong&gt;SetupDiDestroyDriverInfoList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroydriverinfolist)"><strong>SetupDiDestroyDriverInfoList</strong></a></p></td>
<td align="left"><p>ドライバー情報リストを破棄します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-driver-selection-functions-dg"></a>ドライバー選択機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiaskforoemdisk" data-raw-source="[&lt;strong&gt;SetupDiAskForOEMDisk&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiaskforoemdisk)"><strong>SetupDiAskForOEMDisk</strong></a></p></td>
<td align="left"><p>OEM インストールディスクのパスをユーザーに確認するダイアログを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectoemdrv" data-raw-source="[&lt;strong&gt;SetupDiSelectOEMDrv&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectoemdrv)"><strong>SetupDiSelectOEMDrv</strong></a></p></td>
<td align="left"><p>ユーザーが指定した OEM パスを使用して、デバイスのドライバーを選択します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 要求の既定のハンドラー。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-installation-handlers-dg"></a>デバイスのインストールハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller" data-raw-source="[&lt;strong&gt;SetupDiCallClassInstaller&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)"><strong>SetupDiCallClassInstaller</strong></a></p></td>
<td align="left"><p>指定したインストール要求を使用して、適切なクラスインストーラーと登録されているすべての共同インストーラーを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate" data-raw-source="[&lt;strong&gt;SetupDiChangeState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)"><strong>SetupDiChangeState</strong></a></p></td>
<td align="left"><p>DIF_PROPERTYCHANGE 要求の既定のハンドラー。 インストールされているデバイスの状態を変更するために使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers" data-raw-source="[&lt;strong&gt;SetupDiRegisterCoDeviceInstallers&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers)"><strong>SetupDiRegisterCoDeviceInstallers</strong></a></p></td>
<td align="left"><p>指定されたデバイスの INF ファイルに記載されているデバイス固有の共同インストーラーを登録します。 この関数は、DIF_REGISTER_COINSTALLERS の既定のハンドラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice" data-raw-source="[&lt;strong&gt;SetupDiInstallDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)"><strong>SetupDiInstallDevice</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles" data-raw-source="[&lt;strong&gt;SetupDiInstallDriverFiles&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)"><strong>SetupDiInstallDriverFiles</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICEFILES 要求の既定のハンドラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>DIF_INSTALLINTERFACES 要求の既定のハンドラー。 これにより、 <em>Ddinstall</em>に記載されているインターフェイスがインストールされます。デバイスの INF ファイルの<strong>インターフェイス</strong>セクション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/install/setupdimoveduplicatedevice" data-raw-source="[&lt;strong&gt;SetupDiMoveDuplicateDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/install/setupdimoveduplicatedevice)"><strong>SetupDiMoveDuplicateDevice</strong></a></p></td>
<td align="left"><p>この関数は互換性のために残されていますが、どのバージョンの Microsoft Windows でも使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice" data-raw-source="[&lt;strong&gt;SetupDiRemoveDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)"><strong>SetupDiRemoveDevice</strong></a></p></td>
<td align="left"><p>DIF_REMOVEDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice" data-raw-source="[&lt;strong&gt;SetupDiUnremoveDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiunremovedevice)"><strong>SetupDiUnremoveDevice</strong></a></p></td>
<td align="left"><p>DIF_UNREMOVE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>DIF_REGISTERDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectdevice)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv" data-raw-source="[&lt;strong&gt;SetupDiSelectBestCompatDrv&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)"><strong>SetupDiSelectBestCompatDrv</strong></a></p></td>
<td align="left"><p>DIF_SELECTBESTCOMPATDRV 要求の既定のハンドラー。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-installation-customization-functions-dg"></a>デバイスのインストールのカスタマイズ機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiGetClassInstallParams&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassinstallparamsa)"><strong>SetupDiGetClassInstallParams</strong></a></p></td>
<td align="left"><p>デバイス情報セットまたは特定のデバイス情報要素のクラスインストールパラメーターを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiSetClassInstallParams&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassinstallparamsa)"><strong>SetupDiSetClassInstallParams</strong></a></p></td>
<td align="left"><p>デバイス情報セットまたは特定のデバイス情報要素のクラスインストールパラメーターを設定またはクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstallParams&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinstallparamsa)"><strong>SetupDiGetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>デバイス情報セットまたは特定のデバイス情報要素のデバイスインストールパラメーターを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInstallParams&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)"><strong>SetupDiSetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>デバイス情報セットまたは特定のデバイス情報要素のデバイスインストールパラメーターを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInstallParams&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)"><strong>SetupDiGetDriverInstallParams</strong></a></p></td>
<td align="left"><p>指定されたドライバーのインストールパラメーターを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa" data-raw-source="[&lt;strong&gt;SetupDiSetDriverInstallParams&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa)"><strong>SetupDiSetDriverInstallParams</strong></a></p></td>
<td align="left"><p>指定されたドライバーのインストールパラメーターを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-setup-class-functions-dg"></a>セットアップクラスの関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolist" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolist)"><strong>SetupDiBuildClassInfoList</strong></a></p></td>
<td align="left"><p>システムにインストールされているすべてのクラスを含むセットアップクラス Guid の一覧を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoListEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuildclassinfolistexa)"><strong>Setupdibuildclassinの Istex</strong></a></p></td>
<td align="left"><p>ローカルシステムまたはリモートシステムにインストールされているすべてのクラスを含むセットアップクラス Guid の一覧を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptiona" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescription&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptiona)"><strong>SetupDiGetClassDescription</strong></a></p></td>
<td align="left"><p>指定されたセットアップクラス GUID に関連付けられているクラスの説明を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescriptionEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdescriptionexa)"><strong>SetupDiGetClassDescriptionEx</strong></a></p></td>
<td align="left"><p>ローカルコンピューターまたはリモートコンピューターにインストールされているセットアップクラスの説明を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetinfclassa" data-raw-source="[&lt;strong&gt;SetupDiGetINFClass&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetinfclassa)"><strong>SetupDiGetINFClass</strong></a></p></td>
<td align="left"><p>指定したデバイスの INF ファイルのクラスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnamea" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromName&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnamea)"><strong>SetupDiClassGuidsFromName</strong></a></p></td>
<td align="left"><p>指定したクラス名に関連付けられている Guid を取得します。 この一覧は、システムに現在インストールされているクラスに基づいて作成されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnameexa" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromNameEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassguidsfromnameexa)"><strong>SetupDiClassGuidsFromNameEx</strong></a></p></td>
<td align="left"><p>指定したクラス名に関連付けられている Guid を取得します。 この結果の一覧には、ローカルコンピューターまたはリモートコンピューターに現在インストールされているクラスが含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuid&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida)"><strong>SetupDiClassNameFromGuid</strong></a></p></td>
<td align="left"><p>クラス GUID に関連付けられているクラス名を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguidexa" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuidEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguidexa)"><strong>SetupDiClassNameFromGuidEx</strong></a></p></td>
<td align="left"><p>クラス GUID に関連付けられているクラス名を取得します。 クラスは、ローカルコンピューターまたはリモートコンピューターにインストールできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassa" data-raw-source="[&lt;strong&gt;SetupDiInstallClass&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassa)"><strong>SetupDiInstallClass</strong></a></p></td>
<td align="left"><p>指定された INF ファイルの<strong>ClassInstall32</strong>セクションをインストールします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>クラスインストーラーまたはインターフェイスクラスをインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p><a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">デバイスセットアップクラス</a>のレジストリキー、またはクラスの特定のサブキーを開きます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスのレジストリキー、デバイスインターフェイスクラスのレジストリキー、またはクラスの特定のサブキーを開きます。 この関数は、ローカルコンピューターまたはリモートコンピューター上の指定されたキーを開きます。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-class-bitmap-and-icon-functions-dg"></a>ビットマップおよびアイコンの関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelist" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelist)"><strong>SetupDiGetClassImageList</strong></a></p></td>
<td align="left"><p>インストールされているすべてのクラスのビットマップを含むイメージリストを構築し、データ構造体のリストを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelistexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageListEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimagelistexa)"><strong>SetupDiGetClassImageListEx</strong></a></p></td>
<td align="left"><p>ローカルコンピューターまたはリモートコンピューターにインストールされているすべてのクラスのビットマップのイメージリストを構築します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimageindex" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageIndex&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassimageindex)"><strong>SetupDiGetClassImageIndex</strong></a></p></td>
<td align="left"><p>指定したクラスのクラスイメージリスト内のインデックスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassbitmapindex" data-raw-source="[&lt;strong&gt;SetupDiGetClassBitmapIndex&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassbitmapindex)"><strong>SetupDiGetClassBitmapIndex</strong></a></p></td>
<td align="left"><p>指定したクラスに対して提供されるミニアイコンのインデックスを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon" data-raw-source="[&lt;strong&gt;SetupDiDrawMiniIcon&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidrawminiicon)"><strong>SetupDiDrawMiniIcon</strong></a></p></td>
<td align="left"><p>要求された位置に、指定したミニアイコンを描画します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon" data-raw-source="[&lt;strong&gt;SetupDiLoadClassIcon&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloadclassicon)"><strong>SetupDiLoadClassIcon</strong></a></p></td>
<td align="left"><p>指定したクラスの大きいアイコンとミニアイコンの両方を読み込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloaddeviceicon" data-raw-source="[&lt;strong&gt;SetupDiLoadDeviceIcon&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiloaddeviceicon)"><strong>SetupDiLoadDeviceIcon</strong></a></p></td>
<td align="left"><p>指定されたデバイスのデバイスアイコンを読み込みます。 (Windows Vista 以降のバージョンの Windows)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroyclassimagelist" data-raw-source="[&lt;strong&gt;SetupDiDestroyClassImageList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdidestroyclassimagelist)"><strong>SetupDiDestroyClassImageList</strong></a></p></td>
<td align="left"><p>クラスイメージリストを破棄します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-interface-functions-dg"></a>デバイスインターフェイス関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfacea)"><strong>SetupDiCreateDeviceInterface</strong></a></p></td>
<td align="left"><p>デバイスのデバイス機能 (デバイスインターフェイス) を登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfacea" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfacea)"><strong>SetupDiOpenDeviceInterface</strong></a></p></td>
<td align="left"><p>既存のデバイスインターフェイスに関する情報を取得し、指定したデバイス情報セットに追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacealias" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceAlias&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacealias)"><strong>SetupDiGetDeviceInterfaceAlias</strong></a></p></td>
<td align="left"><p>指定されたデバイスインターフェイスのエイリアスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>指定されたクラスのすべてのデバイスを含むデバイス情報セットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>ローカルコンピューターまたはリモートコンピューター上の指定されたクラスのすべてのデバイスを含むデバイス情報セットを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInterfaces&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)"><strong>SetupDiEnumDeviceInterfaces</strong></a></p></td>
<td align="left"><p>デバイス情報セットのデバイスインターフェイス要素のコンテキスト構造体を返します。 各呼び出しは、1つのデバイスインターフェイスに関する情報を返します。</p>
<p>関数を繰り返し呼び出して、1つまたは複数のデバイスによって公開されている複数のインターフェイスに関する情報を取得することができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceDetail&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacedetaila)"><strong>SetupDiGetDeviceInterfaceDetail</strong></a></p></td>
<td align="left"><p>特定のデバイスインターフェイスに関する詳細を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスインスタンスに関する情報を格納するためのレジストリサブキーを作成し、そのキーへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスインスタンスに固有の情報を格納するためにアプリケーションとドライバーによって使用されるレジストリサブキーを開き、キーへのハンドルを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスインスタンスに固有の情報を格納するために、アプリケーションとドライバーによって使用されたレジストリサブキーを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>DIF_INSTALLINTERFACES 要求の既定のハンドラーです。 これにより、 <em>Ddinstall</em>に記載されているインターフェイスがインストールされます。デバイスの INF ファイルの<strong>インターフェイス</strong>セクション。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedeviceinterface" data-raw-source="[&lt;strong&gt;SetupDiRemoveDeviceInterface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedeviceinterface)"><strong>SetupDiRemoveDeviceInterface</strong></a></p></td>
<td align="left"><p>登録されているデバイスインターフェイスをシステムから削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfacedata" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceData&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfacedata)"><strong>SetupDiDeleteDeviceInterfaceData</strong></a></p></td>
<td align="left"><p>デバイス情報セットからデバイスインターフェイスを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacedefault" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceDefault&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacedefault)"><strong>SetupDiSetDeviceInterfaceDefault</strong></a></p></td>
<td align="left"><p>デバイスクラスの既定のインターフェイスとして、指定されたデバイスインターフェイスを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstallclassexa)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>クラスインストーラーまたはインターフェイスクラスをインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p><a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">デバイスセットアップクラス</a>のレジストリキー、デバイスインターフェイスクラスのレジストリキー、またはクラスの特定のサブキーを開きます。 この関数は、ローカルコンピューターまたはリモートコンピューター上の指定されたキーを開きます。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-property-functions-dg"></a>デバイスプロパティ関数 (Windows Vista 以降)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw" data-raw-source="[&lt;strong&gt;SetupDiGetClassProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)"><strong>SetupDiGetClassProperty</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスまたはデバイスインターフェイスクラスに設定されているデバイスプロパティを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)"><strong>SetupDiGetClassPropertyEx</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスまたはローカルコンピューターまたはリモートコンピューター上のデバイスインターフェイスクラスのクラスプロパティを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeys&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeys)"><strong>SetupDiGetClassPropertyKeys</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスまたはデバイスインターフェイスクラスに設定されているデバイスプロパティを表すデバイスプロパティキーの配列を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeysEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertykeysexw)"><strong>Setupdigetclasspropertysex</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスまたはローカルコンピューターまたはリモートコンピューター上のデバイスインターフェイスクラスに設定されているデバイスプロパティを表すデバイスプロパティキーの配列を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)"><strong>SetupDiGetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスに設定されているデバイスプロパティを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfacePropertyKeys&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertykeys)"><strong>SetupDiGetDeviceInterfacePropertyKeys</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスに設定されているデバイスプロパティを表すデバイスプロパティキーの配列を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)"><strong>SetupDiGetDeviceProperty</strong></a></p></td>
<td align="left"><p>デバイスインスタンスプロパティを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys" data-raw-source="[&lt;strong&gt;SetupDiGetDevicePropertyKeys&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)"><strong>SetupDiGetDevicePropertyKeys</strong></a></p></td>
<td align="left"><p>デバイスインスタンスに設定されているデバイスプロパティを表すデバイスプロパティキーの配列を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw" data-raw-source="[&lt;strong&gt;SetupDiSetClassProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyw)"><strong>SetupDiSetClassProperty</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスまたはデバイスインターフェイスクラスのクラスプロパティを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw" data-raw-source="[&lt;strong&gt;SetupDiSetClassPropertyEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclasspropertyexw)"><strong>SetupDiSetClassPropertyEx</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスまたはローカルコンピューターまたはリモートコンピューター上のデバイスインターフェイスクラスのデバイスプロパティを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)"><strong>SetupDiSetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスのデバイスプロパティを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)"><strong>SetupDiSetDeviceProperty</strong></a></p></td>
<td align="left"><p>デバイスインスタンスプロパティを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-registry-functions-dg"></a>レジストリ関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya" data-raw-source="[&lt;strong&gt;SetupDiCreateDevRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)"><strong>SetupDiCreateDevRegKey</strong></a></p></td>
<td align="left"><p>デバイス固有の構成情報のレジストリストレージキーを作成し、キーへのハンドルを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenDevRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)"><strong>SetupDiOpenDevRegKey</strong></a></p></td>
<td align="left"><p>デバイス固有の構成情報のレジストリストレージキーを開き、キーへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedevregkey" data-raw-source="[&lt;strong&gt;SetupDiDeleteDevRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedevregkey)"><strong>SetupDiDeleteDevRegKey</strong></a></p></td>
<td align="left"><p>デバイス情報要素に関連付けられている、指定したユーザーがアクセスできるレジストリキーを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p>セットアップクラスのレジストリキー、またはクラスの特定のサブキーを開きます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>デバイスセットアップクラスのレジストリキー、デバイスインターフェイスクラスのレジストリキー、またはクラスの特定のサブキーを開きます。</p>
<p>この関数は、ローカルコンピューターまたはリモートコンピューター上の指定されたキーを開きます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinterfaceregkeya)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスインスタンスに関する情報を格納するための不揮発性のレジストリサブキーを作成し、そのキーへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスインスタンスに固有の情報を格納するためにアプリケーションとドライバーによって使用されるレジストリサブキーを開き、キーへのハンドルを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdideletedeviceinterfaceregkey)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイスインターフェイスインスタンスに固有の情報を格納するために、アプリケーションとドライバーによって使用されたレジストリサブキーを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceRegistryProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)"><strong>SetupDiSetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>指定されたプラグアンドプレイデバイスプロパティを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceRegistryProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)"><strong>SetupDiGetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>指定されたプラグアンドプレイデバイスプロパティを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiGetClassRegistryProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)"><strong>SetupDiGetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>指定されたデバイスクラスプロパティをレジストリから取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya" data-raw-source="[&lt;strong&gt;SetupDiSetClassRegistryProperty&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)"><strong>SetupDiSetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>指定されたデバイスクラスプロパティをレジストリに設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-other-setupdi-functions-dg"></a>その他の関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualmodelssectiona" data-raw-source="[&lt;strong&gt;SetupDiGetActualModelsSection&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualmodelssectiona)"><strong>SetupDiGetActualModelsSection</strong></a></p></td>
<td align="left"><p>デバイスの INF ファイルからデバイスをインストールするときに使用する、適切な修飾された<a href="inf-models-section.md" data-raw-source="[&lt;strong&gt;INF Models section&lt;/strong&gt;](inf-models-section.md)"><strong>INF モデルセクション</strong></a>を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstalla" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstall&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstalla)"><strong>SetupDiGetActualSectionToInstall</strong></a></p></td>
<td align="left"><p>デバイスの INF ファイルからデバイスをインストールするときに使用する、適切な<em>Ddinstall</em>セクションを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstallexa" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstallEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetactualsectiontoinstallexa)"><strong>SetupDiGetActualSectionToInstallEx</strong></a></p></td>
<td align="left"><p>指定されたオペレーティングシステムおよびプロセッサアーキテクチャのデバイスをインストールする INF <em>Ddinstall</em>セクションの名前を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynamea" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyName&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynamea)"><strong>SetupDiGetHwProfileFriendlyName</strong></a></p></td>
<td align="left"><p>ハードウェアプロファイル ID に関連付けられたフレンドリ名を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynameexa" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyNameEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilefriendlynameexa)"><strong>SetupDiGetHwProfileFriendlyNameEx</strong></a></p></td>
<td align="left"><p>ローカルコンピューターまたはリモートコンピューターのハードウェアプロファイル ID に関連付けられているフレンドリ名を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelist" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileList&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelist)"><strong>SetupDiGetHwProfileList</strong></a></p></td>
<td align="left"><p>現在定義されているすべてのハードウェアプロファイル Id の一覧を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelistexa" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileListEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigethwprofilelistexa)"><strong>SetupDiGetHwProfileListEx</strong></a></p></td>
<td align="left"><p>ローカルコンピューターまたはリモートコンピューターで現在定義されているすべてのハードウェアプロファイル Id の一覧を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdirestartdevices" data-raw-source="[&lt;strong&gt;SetupDiRestartDevices&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdirestartdevices)"><strong>SetupDiRestartDevices</strong></a></p></td>
<td align="left"><p>指定されたデバイスを再起動するか、必要に応じて、指定されたデバイスと同じ機能とフィルタードライバーによって動作するすべてのデバイスを起動します。</p></td>
</tr>
</tbody>
</table>

 

 

 





