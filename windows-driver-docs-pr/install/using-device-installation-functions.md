---
title: デバイス インストールの機能を使用します。
description: デバイス インストールの機能を使用します。
ms.assetid: a7cfa359-a45c-45fa-a854-ee70de66b12e
keywords:
- SetupAPI 関数 WDK、デバイスのインストール機能
- デバイスのインストールは、WDK SetupAPI を関数します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789460aaeccb5afbcc00495475dd51f355762446
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559876"
---
# <a name="using-device-installation-functions"></a>デバイス インストールの機能を使用します。





このセクションをまとめたものです、[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff541299)します。 デバイス インストールの機能を使用すると、インストール ソフトウェアは、次の種類の操作を実行できます。

-   ドライバーをインストールします。

-   差分のコードを処理します。

-   デバイス情報設定を管理します。

-   ドライバーの一覧を管理します。

-   デバイスのインターフェイスを管理します。

-   アイコンとその他のビットマップを管理します。

このセクションで説明した SetupAPI 関数でサポートされていないデバイスのインストールの操作を実行する適切な呼び出し[一般的なセットアップ関数](https://msdn.microsoft.com/library/windows/hardware/ff544985)または[PnP の Configuration Manager 機能](https://msdn.microsoft.com/library/windows/hardware/ff549717)(Cm _*Xxx*関数<em>)。</em>

次の表では、次の種類の関数の概要を提供します。

[ドライバーのインストール機能](#ddk-update-driver-function-dg)

[デバイス情報関数](#ddk-setupdi-device-information-functions-dg)

[ドライバー情報関数](#ddk-setupdi-driver-information-functions-dg)

[ドライバーの選択関数](#ddk-setupdi-driver-selection-functions-dg)

[デバイス インストールのハンドラー](#ddk-setupdi-device-installation-handlers-dg)

[デバイス インストールのカスタマイズ機能](#ddk-setupdi-device-installation-customization-functions-dg)

[セットアップ クラス関数](#ddk-setupdi-setup-class-functions-dg)

[ビットマップとアイコン関数](#ddk-setupdi-class-bitmap-and-icon-functions-dg)

[デバイス インターフェイス関数](#ddk-setupdi-device-interface-functions-dg)

[プロパティ関数のデバイス (Windows Vista 以降)](#ddk-setupdi-device-property-functions-dg)

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544710" data-raw-source="[&lt;strong&gt;DiInstallDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544710)"><strong>DiInstallDevice</strong></a></p></td>
<td align="left"><p>プレインストールされている指定されたドライバーをインストール、<a href="driver-store.md" data-raw-source="[driver store](driver-store.md)">ドライバー ストア</a>PnP デバイス、システムに存在します。 (Windows Vista および Windows の以降のバージョン)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544717" data-raw-source="[&lt;strong&gt;DiInstallDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544717)"><strong>DiInstallDriver</strong></a></p></td>
<td align="left"><p>ドライバー ストア内のドライバーがプレインストールして、システムに存在する PnP デバイスと一致するドライバーをインストールします。 (Windows Vista および Windows の以降のバージョン)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544721" data-raw-source="[&lt;strong&gt;DiRollbackDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544721)"><strong>DiRollbackDriver</strong></a></p></td>
<td align="left"><p>バックアップ デバイスのドライバーに指定されたデバイスにインストールされているドライバーをロールバックします。 (Windows Vista および Windows の以降のバージョン)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544727" data-raw-source="[&lt;strong&gt;DiShowUpdateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544727)"><strong>DiShowUpdateDevice</strong></a></p></td>
<td align="left"><p>指定したデバイスのハードウェアの更新ウィザードが表示されます。 (Windows Vista および Windows の以降のバージョン)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544754" data-raw-source="[&lt;strong&gt;DiUninstallDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544754)"><strong>DiUninstallDevice</strong></a></p></td>
<td align="left"><p>デバイスをアンインストールし、[デバイス] ノードを削除します (<a href="https://msdn.microsoft.com/library/windows/hardware/ff556277#wdkgloss-devnode" data-raw-source="&lt;em&gt;devnode&lt;/em&gt;"><em>devnode</em></a>))、システムからです。 (Windows 7 および Windows の以降のバージョン)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547654" data-raw-source="[&lt;strong&gt;InstallSelectedDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547654)"><strong>InstallSelectedDriver</strong></a></p></td>
<td align="left"><p>選択したデバイスで、選択したドライバーをインストールします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553534" data-raw-source="[&lt;strong&gt;UpdateDriverForPlugAndPlayDevices&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553534)"><strong>UpdateDriverForPlugAndPlayDevices</strong></a></p></td>
<td align="left"><p>照合システムに存在する PnP デバイスのインストールされている関数のドライバーを更新します。</p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550956" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550956)"><strong>SetupDiCreateDeviceInfoList</strong></a></p></td>
<td align="left"><p>空を作成します。<a href="device-information-sets.md" data-raw-source="[device information set](device-information-sets.md)">デバイス情報設定されている</a>します。 このセットは、クラスの GUID を関連付けることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550958" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfoListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550958)"><strong>SetupDiCreateDeviceInfoListEx</strong></a></p></td>
<td align="left"><p>空のデバイスの情報セットを作成します。 このセットはクラス GUID を関連付けることができ、リモート コンピューター上のデバイスを指定できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550952" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550952)"><strong>SetupDiCreateDeviceInfo</strong></a></p></td>
<td align="left"><p>新しいデバイス情報の要素を作成し、指定したデバイスの情報セットに新しいメンバーとして追加します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552071" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552071)"><strong>SetupDiOpenDeviceInfo</strong></a></p></td>
<td align="left"><p>デバイスの既存のインスタンスに関する情報を取得し、それを指定したデバイスの情報セットに追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551010" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551010)"><strong>SetupDiEnumDeviceInfo</strong></a></p></td>
<td align="left"><p>デバイス情報の一連のデバイス情報の要素のコンテキストの構造を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551106" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstanceId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551106)"><strong>SetupDiGetDeviceInstanceId</strong></a></p></td>
<td align="left"><p>デバイス情報の要素に関連付けられたデバイス インスタンス ID を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551101" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListClass&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551101)"><strong>SetupDiGetDeviceInfoListClass</strong></a></p></td>
<td align="left"><p>関連付けられたクラスがある場合は、設定、デバイスの情報に関連付けられている GUID クラスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551103" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInfoListDetail&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551103)"><strong>SetupDiGetDeviceInfoListDetail</strong></a></p></td>
<td align="left"><p>クラス GUID、リモート コンピューターのハンドル、およびリモート コンピューターの名前を含む設定のデバイス情報に関連付けられている情報を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551064" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevPropertySheets&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551064)"><strong>SetupDiGetClassDevPropertySheets</strong></a></p></td>
<td align="left"><p>指定したデバイス情報の要素またはプロパティ シートへのハンドルを取得、<a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">デバイス セットアップ クラス</a>の指定したデバイス情報の設定。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551069" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551069)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>指定したクラスのすべてのデバイスを含むデバイス情報のセットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551072" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551072)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>ローカルまたはリモート コンピューター上の指定したクラスのすべてのデバイスを含むデバイス情報のセットを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552176" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552176)"><strong>SetupDiSetSelectedDevice</strong></a></p></td>
<td align="left"><p>デバイス情報の現在選択されているメンバーである指定されたデバイス情報要素セットを設定します。 この関数は、通常、インストール ウィザードによって使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552011" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552011)"><strong>SetupDiGetSelectedDevice</strong></a></p></td>
<td align="left"><p>指定したデバイスの情報セットについては、現在選択されているデバイスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552091" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552091)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>プラグ アンド プレイのマネージャーを新しく作成したデバイスのインスタンスを登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550978" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550978)"><strong>SetupDiDeleteDeviceInfo</strong></a></p></td>
<td align="left"><p>指定したデバイス情報のセットからメンバーを削除します。 この関数では、実際のデバイスは削除されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550996" data-raw-source="[&lt;strong&gt;SetupDiDestroyDeviceInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550996)"><strong>SetupDiDestroyDeviceInfoList</strong></a></p></td>
<td align="left"><p>デバイス情報のセットを破棄し、関連付けられているすべてのメモリを解放します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-driver-information-functions-dg"></a>ドライバー情報関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550917" data-raw-source="[&lt;strong&gt;SetupDiBuildDriverInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550917)"><strong>SetupDiBuildDriverInfoList</strong></a></p></td>
<td align="left"><p>デバイスの情報セットまたは指定したデバイスのインスタンスと関連付けられたドライバーのリストを構築&#39;s グローバル クラス ドライバーの一覧。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551018" data-raw-source="[&lt;strong&gt;SetupDiEnumDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551018)"><strong>SetupDiEnumDriverInfo</strong></a></p></td>
<td align="left"><p>ドライバー情報のリストのメンバーを列挙します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551973" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInfoDetail&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551973)"><strong>SetupDiGetDriverInfoDetail</strong></a></p></td>
<td align="left"><p>指定されたドライバー情報の要素の詳細な情報を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552183" data-raw-source="[&lt;strong&gt;SetupDiSetSelectedDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552183)"><strong>SetupDiSetSelectedDriver</strong></a></p></td>
<td align="left"><p>ドライバーの一覧の指定されたメンバーを現在選択されているドライバーとして設定します。 現在選択されているドライバーがないように、ドライバーのリストをリセットすることにも使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552013" data-raw-source="[&lt;strong&gt;SetupDiGetSelectedDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552013)"><strong>SetupDiGetSelectedDriver</strong></a></p></td>
<td align="left"><p>インストールするドライバーとして選択したドライバーの一覧のメンバーを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550928" data-raw-source="[&lt;strong&gt;SetupDiCancelDriverInfoSearch&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550928)"><strong>SetupDiCancelDriverInfoSearch</strong></a></p></td>
<td align="left"><p>現在進行中にある別のスレッド ドライバー一覧の検索を取り消します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551001" data-raw-source="[&lt;strong&gt;SetupDiDestroyDriverInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551001)"><strong>SetupDiDestroyDriverInfoList</strong></a></p></td>
<td align="left"><p>ドライバー情報のリストを破棄します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-driver-selection-functions-dg"></a>ドライバーの選択関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550905" data-raw-source="[&lt;strong&gt;SetupDiAskForOEMDisk&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550905)"><strong>SetupDiAskForOEMDisk</strong></a></p></td>
<td align="left"><p>OEM インストール ディスクのパスをユーザーに確認ダイアログが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552121" data-raw-source="[&lt;strong&gt;SetupDiSelectOEMDrv&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552121)"><strong>SetupDiSelectOEMDrv</strong></a></p></td>
<td align="left"><p>ユーザーによって提供される OEM のパスを使用して、デバイスのドライバーを選択します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552115" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552115)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 要求の既定のハンドラー。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-installation-handlers-dg"></a>デバイス インストールのハンドラー

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550922" data-raw-source="[&lt;strong&gt;SetupDiCallClassInstaller&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550922)"><strong>SetupDiCallClassInstaller</strong></a></p></td>
<td align="left"><p>適切なクラスのインストーラーを呼び出すと、指定したインストールの要求で共同インストーラーは、登録されているいずれか。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550930" data-raw-source="[&lt;strong&gt;SetupDiChangeState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550930)"><strong>SetupDiChangeState</strong></a></p></td>
<td align="left"><p>DIF_PROPERTYCHANGE 要求の既定のハンドラー。 インストール済みのデバイスの状態を変更するために使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552085" data-raw-source="[&lt;strong&gt;SetupDiRegisterCoDeviceInstallers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552085)"><strong>SetupDiRegisterCoDeviceInstallers</strong></a></p></td>
<td align="left"><p>デバイスに固有の共同インストーラー INF ファイルに、指定されたデバイスを登録します。 この関数は、DIF_REGISTER_COINSTALLERS の既定のハンドラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552039" data-raw-source="[&lt;strong&gt;SetupDiInstallDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552039)"><strong>SetupDiInstallDevice</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552048" data-raw-source="[&lt;strong&gt;SetupDiInstallDriverFiles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552048)"><strong>SetupDiInstallDriverFiles</strong></a></p></td>
<td align="left"><p>DIF_INSTALLDEVICEFILES 要求の既定のハンドラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552043" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552043)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>DIF_INSTALLINTERFACES 要求の既定のハンドラー。 記載されているインターフェイスのインストール、 <em>DDInstall</em>.<strong>インターフェイス</strong>デバイス INF ファイルのセクション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552062" data-raw-source="[&lt;strong&gt;SetupDiMoveDuplicateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552062)"><strong>SetupDiMoveDuplicateDevice</strong></a></p></td>
<td align="left"><p>この関数は廃止され、Microsoft Windows の任意のバージョンでは使用できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552097" data-raw-source="[&lt;strong&gt;SetupDiRemoveDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552097)"><strong>SetupDiRemoveDevice</strong></a></p></td>
<td align="left"><p>DIF_REMOVEDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552193" data-raw-source="[&lt;strong&gt;SetupDiUnremoveDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552193)"><strong>SetupDiUnremoveDevice</strong></a></p></td>
<td align="left"><p>DIF_UNREMOVE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552091" data-raw-source="[&lt;strong&gt;SetupDiRegisterDeviceInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552091)"><strong>SetupDiRegisterDeviceInfo</strong></a></p></td>
<td align="left"><p>DIF_REGISTERDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552115" data-raw-source="[&lt;strong&gt;SetupDiSelectDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552115)"><strong>SetupDiSelectDevice</strong></a></p></td>
<td align="left"><p>DIF_SELECTDEVICE 要求の既定のハンドラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552112" data-raw-source="[&lt;strong&gt;SetupDiSelectBestCompatDrv&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552112)"><strong>SetupDiSelectBestCompatDrv</strong></a></p></td>
<td align="left"><p>DIF_SELECTBESTCOMPATDRV 要求の既定のハンドラー。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-installation-customization-functions-dg"></a>デバイス インストールのカスタマイズ機能

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551083" data-raw-source="[&lt;strong&gt;SetupDiGetClassInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551083)"><strong>SetupDiGetClassInstallParams</strong></a></p></td>
<td align="left"><p>デバイスの情報セットまたは特定のデバイス情報の要素のクラスのインストール パラメーターを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552122" data-raw-source="[&lt;strong&gt;SetupDiSetClassInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552122)"><strong>SetupDiSetClassInstallParams</strong></a></p></td>
<td align="left"><p>設定またはデバイスの情報セットまたは特定のデバイス情報の要素のクラスのインストール パラメーターを消去します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551104" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551104)"><strong>SetupDiGetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>デバイスの情報セットまたは特定のデバイス情報の要素のデバイスのインストール パラメーターを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552141" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552141)"><strong>SetupDiSetDeviceInstallParams</strong></a></p></td>
<td align="left"><p>デバイスの情報セットまたは特定のデバイス情報の要素のデバイスのインストール パラメーターを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551978" data-raw-source="[&lt;strong&gt;SetupDiGetDriverInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551978)"><strong>SetupDiGetDriverInstallParams</strong></a></p></td>
<td align="left"><p>取得しますが、指定したドライバーのパラメーターをインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552172" data-raw-source="[&lt;strong&gt;SetupDiSetDriverInstallParams&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552172)"><strong>SetupDiSetDriverInstallParams</strong></a></p></td>
<td align="left"><p>指定されたドライバーのインストール パラメーターを設定します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-setup-class-functions-dg"></a>セットアップ クラス関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550909" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550909)"><strong>SetupDiBuildClassInfoList</strong></a></p></td>
<td align="left"><p>セットアップの一覧に、システムにインストールされているすべてのクラスを含むクラス Guid を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550911" data-raw-source="[&lt;strong&gt;SetupDiBuildClassInfoListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550911)"><strong>SetupDiBuildClassInfoListEx</strong></a></p></td>
<td align="left"><p>セットアップの一覧をローカル システムまたはリモート システムにインストールされているすべてのクラスを含むクラス Guid を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551053" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescription&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551053)"><strong>SetupDiGetClassDescription</strong></a></p></td>
<td align="left"><p>指定したセットアップ クラス GUID に関連付けられているクラスの説明を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551058" data-raw-source="[&lt;strong&gt;SetupDiGetClassDescriptionEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551058)"><strong>SetupDiGetClassDescriptionEx</strong></a></p></td>
<td align="left"><p>ローカルまたはリモート コンピューターにインストールされているセットアップ クラスの説明を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552010" data-raw-source="[&lt;strong&gt;SetupDiGetINFClass&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552010)"><strong>SetupDiGetINFClass</strong></a></p></td>
<td align="left"><p>指定したデバイスの INF ファイルのクラスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550937" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550937)"><strong>SetupDiClassGuidsFromName</strong></a></p></td>
<td align="left"><p>指定されたクラス名に関連付けられている Guid を取得します。 この一覧は、システムに現在インストールされているどのようなクラスをベースに作成されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550941" data-raw-source="[&lt;strong&gt;SetupDiClassGuidsFromNameEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550941)"><strong>SetupDiClassGuidsFromNameEx</strong></a></p></td>
<td align="left"><p>指定されたクラス名に関連付けられている Guid を取得します。 この結果のリストには、ローカルまたはリモート コンピューターに現在インストールされているクラスが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550947" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuid&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550947)"><strong>SetupDiClassNameFromGuid</strong></a></p></td>
<td align="left"><p>クラスの GUID に関連付けられたクラス名を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550950" data-raw-source="[&lt;strong&gt;SetupDiClassNameFromGuidEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550950)"><strong>SetupDiClassNameFromGuidEx</strong></a></p></td>
<td align="left"><p>クラスの GUID に関連付けられたクラス名を取得します。 クラスは、ローカルまたはリモート コンピューターにインストールできます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552024" data-raw-source="[&lt;strong&gt;SetupDiInstallClass&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552024)"><strong>SetupDiInstallClass</strong></a></p></td>
<td align="left"><p>インストール、 <strong>ClassInstall32</strong>指定した INF ファイルのセクション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552032" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552032)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>クラスのインストーラーまたはインターフェイス クラスをインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552065" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552065)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p>開く、<a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">デバイス セットアップ クラス</a>レジストリ キー、またはクラスの特定のサブキー。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552067" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552067)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>デバイス セットアップ クラスのレジストリ キー、デバイス インターフェイス クラスのレジストリ キーまたはクラスの特定のサブキーを開きます。 この機能は、ローカル コンピューターまたはリモート コンピューター上の指定したキーを開きます。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-class-bitmap-and-icon-functions-dg"></a>ビットマップとアイコン関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551080" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551080)"><strong>SetupDiGetClassImageList</strong></a></p></td>
<td align="left"><p>イメージ リストをすべてインストールされているクラス用のビットマップを含み、データ構造の一覧を返しますを構築します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551081" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551081)"><strong>SetupDiGetClassImageListEx</strong></a></p></td>
<td align="left"><p>ローカルまたはリモート コンピューターにインストールされているすべてのクラス用のビットマップのイメージ リストを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551074" data-raw-source="[&lt;strong&gt;SetupDiGetClassImageIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551074)"><strong>SetupDiGetClassImageIndex</strong></a></p></td>
<td align="left"><p>指定したクラスのクラスのイメージ リスト内のインデックスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551047" data-raw-source="[&lt;strong&gt;SetupDiGetClassBitmapIndex&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551047)"><strong>SetupDiGetClassBitmapIndex</strong></a></p></td>
<td align="left"><p>指定したクラスの指定された小さいアイコンのインデックスを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551005" data-raw-source="[&lt;strong&gt;SetupDiDrawMiniIcon&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551005)"><strong>SetupDiDrawMiniIcon</strong></a></p></td>
<td align="left"><p>要求された場所に指定された小さいアイコンを描画します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552053" data-raw-source="[&lt;strong&gt;SetupDiLoadClassIcon&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552053)"><strong>SetupDiLoadClassIcon</strong></a></p></td>
<td align="left"><p>両方大きなロードと、指定したクラスのミニ アイコン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552057" data-raw-source="[&lt;strong&gt;SetupDiLoadDeviceIcon&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552057)"><strong>SetupDiLoadDeviceIcon</strong></a></p></td>
<td align="left"><p>指定したデバイスのデバイスのアイコンを読み込みます。 (Windows Vista および Windows の以降のバージョン)</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550995" data-raw-source="[&lt;strong&gt;SetupDiDestroyClassImageList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550995)"><strong>SetupDiDestroyClassImageList</strong></a></p></td>
<td align="left"><p>クラスのイメージ リストを破棄します。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-interface-functions-dg"></a>デバイス インターフェイス関数

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550965" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550965)"><strong>SetupDiCreateDeviceInterface</strong></a></p></td>
<td align="left"><p>デバイスのデバイスの機能 (デバイス インターフェイス) を登録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552074" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552074)"><strong>SetupDiOpenDeviceInterface</strong></a></p></td>
<td align="left"><p>既存のデバイス インターフェイスに関する情報を取得し、指定したデバイスの情報セットに追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551108" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceAlias&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551108)"><strong>SetupDiGetDeviceInterfaceAlias</strong></a></p></td>
<td align="left"><p>指定したデバイスのインターフェイスのエイリアスを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551072" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551072)"><strong>SetupDiGetClassDevs</strong></a></p></td>
<td align="left"><p>指定したクラスのすべてのデバイスを含むデバイス情報のセットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551072" data-raw-source="[&lt;strong&gt;SetupDiGetClassDevsEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551072)"><strong>SetupDiGetClassDevsEx</strong></a></p></td>
<td align="left"><p>ローカルまたはリモート コンピューター上の指定したクラスのすべてのデバイスを含むデバイス情報のセットを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551015" data-raw-source="[&lt;strong&gt;SetupDiEnumDeviceInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551015)"><strong>SetupDiEnumDeviceInterfaces</strong></a></p></td>
<td align="left"><p>デバイス情報の一連のデバイスのインターフェイス要素のコンテキストの構造を返します。 各呼び出しは、1 つのデバイス インターフェイスに関する情報を返します。</p>
<p>関数は、1 つまたは複数のデバイスによって公開されているいくつかのインターフェイスに関する情報を取得する繰り返し呼び出すことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551120" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceDetail&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551120)"><strong>SetupDiGetDeviceInterfaceDetail</strong></a></p></td>
<td align="left"><p>特定のデバイス インターフェイスに関する詳細を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550967" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550967)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイス インターフェイスのインスタンスに関する情報を格納するためのレジストリ サブキーを作成し、キーへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552075" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552075)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイス インターフェイスのインスタンスに固有であり、キーへのハンドルを返しますの情報を格納するアプリケーションやドライバーで使用されるレジストリ サブキーを開きます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550986" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550986)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイス インターフェイスのインスタンスに固有の情報を格納するアプリケーションやドライバーで使用されていたレジストリ サブキーを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552043" data-raw-source="[&lt;strong&gt;SetupDiInstallDeviceInterfaces&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552043)"><strong>SetupDiInstallDeviceInterfaces</strong></a></p></td>
<td align="left"><p>DIF_INSTALLINTERFACES 要求の既定のハンドラーです。 記載されているインターフェイスのインストール、 <em>DDInstall</em>.<strong>インターフェイス</strong>デバイス INF ファイルのセクション。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552102" data-raw-source="[&lt;strong&gt;SetupDiRemoveDeviceInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552102)"><strong>SetupDiRemoveDeviceInterface</strong></a></p></td>
<td align="left"><p>システムから登録済みデバイスのインターフェイスを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550984" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550984)"><strong>SetupDiDeleteDeviceInterfaceData</strong></a></p></td>
<td align="left"><p>デバイス情報のセットからデバイスのインターフェイスを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552149" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceDefault&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552149)"><strong>SetupDiSetDeviceInterfaceDefault</strong></a></p></td>
<td align="left"><p>デバイス クラスに対する既定のインターフェイスとして指定されたデバイスのインターフェイスを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552032" data-raw-source="[&lt;strong&gt;SetupDiInstallClassEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552032)"><strong>SetupDiInstallClassEx</strong></a></p></td>
<td align="left"><p>クラスのインストーラーまたはインターフェイス クラスをインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552067" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552067)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>開く、<a href="device-setup-classes.md" data-raw-source="[device setup class](device-setup-classes.md)">デバイス セットアップ クラス</a>レジストリ キー、デバイス インターフェイス クラスのレジストリ キーまたはクラスの特定のサブキー。 この機能は、ローカル コンピューターまたはリモート コンピューター上の指定したキーを開きます。</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-setupdi-device-property-functions-dg"></a>プロパティ関数のデバイス (Windows Vista 以降)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551086" data-raw-source="[&lt;strong&gt;SetupDiGetClassProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551086)"><strong>SetupDiGetClassProperty</strong></a></p></td>
<td align="left"><p>デバイス セットアップ クラスまたはデバイスのインターフェイス クラスに設定されているデバイス プロパティを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551090" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551090)"><strong>SetupDiGetClassPropertyEx</strong></a></p></td>
<td align="left"><p>デバイス セットアップ クラスまたはローカルまたはリモート コンピューター上のデバイス インターフェイス クラスのクラスのプロパティを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551091" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeys&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551091)"><strong>SetupDiGetClassPropertyKeys</strong></a></p></td>
<td align="left"><p>デバイス セットアップ クラスまたはデバイスのインターフェイス クラスに設定されているデバイスのプロパティを表すデバイス プロパティのキーの配列を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551093" data-raw-source="[&lt;strong&gt;SetupDiGetClassPropertyKeysEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551093)"><strong>SetupDiGetClassPropertyKeysEx</strong></a></p></td>
<td align="left"><p>ローカル デバイス インターフェイスのクラスまたはリモート コンピューターのデバイス セットアップ クラスをまたはに設定されているデバイスのプロパティを表すデバイス プロパティのキーの配列を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551122" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfaceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551122)"><strong>SetupDiGetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>デバイスのインターフェイスが設定されているデバイス プロパティを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551959" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceInterfacePropertyKeys&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551959)"><strong>SetupDiGetDeviceInterfacePropertyKeys</strong></a></p></td>
<td align="left"><p>デバイスのインターフェイスに設定されているデバイスのプロパティを表すデバイス プロパティのキーの配列を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551963" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551963)"><strong>SetupDiGetDeviceProperty</strong></a></p></td>
<td align="left"><p>デバイス インスタンスのプロパティを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551965" data-raw-source="[&lt;strong&gt;SetupDiGetDevicePropertyKeys&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551965)"><strong>SetupDiGetDevicePropertyKeys</strong></a></p></td>
<td align="left"><p>デバイス インスタンスに設定されているデバイスのプロパティを表すデバイス プロパティのキーの配列を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552128" data-raw-source="[&lt;strong&gt;SetupDiSetClassProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552128)"><strong>SetupDiSetClassProperty</strong></a></p></td>
<td align="left"><p>デバイス セットアップ クラスまたはデバイスのインターフェイス クラスのクラスのプロパティを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552132" data-raw-source="[&lt;strong&gt;SetupDiSetClassPropertyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552132)"><strong>SetupDiSetClassPropertyEx</strong></a></p></td>
<td align="left"><p>ローカルまたはリモート コンピューター上のデバイス セットアップ クラスまたはデバイスのインターフェイス クラスのデバイス プロパティを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552158" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceInterfaceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552158)"><strong>SetupDiSetDeviceInterfaceProperty</strong></a></p></td>
<td align="left"><p>デバイス インターフェイスのデバイス プロパティを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552163" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552163)"><strong>SetupDiSetDeviceProperty</strong></a></p></td>
<td align="left"><p>デバイス インスタンスのプロパティを設定します。</p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550973" data-raw-source="[&lt;strong&gt;SetupDiCreateDevRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550973)"><strong>SetupDiCreateDevRegKey</strong></a></p></td>
<td align="left"><p>デバイスに固有の構成情報についてレジストリ ストレージ キーを作成し、キーへのハンドルを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552079" data-raw-source="[&lt;strong&gt;SetupDiOpenDevRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552079)"><strong>SetupDiOpenDevRegKey</strong></a></p></td>
<td align="left"><p>デバイス固有の構成情報のレジストリ キーを記憶域が開き、キーへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550991" data-raw-source="[&lt;strong&gt;SetupDiDeleteDevRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550991)"><strong>SetupDiDeleteDevRegKey</strong></a></p></td>
<td align="left"><p>デバイス情報の要素に関連付けられている指定されたユーザーがアクセスできるレジストリ キーを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552065" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552065)"><strong>SetupDiOpenClassRegKey</strong></a></p></td>
<td align="left"><p>セットアップ クラスのレジストリ キー、またはクラスの特定のサブキーを開きます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552067" data-raw-source="[&lt;strong&gt;SetupDiOpenClassRegKeyEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552067)"><strong>SetupDiOpenClassRegKeyEx</strong></a></p></td>
<td align="left"><p>デバイス セットアップ クラスのレジストリ キー、デバイス インターフェイス クラスのレジストリ キーまたはクラスの特定のサブキーを開きます。</p>
<p>この機能は、ローカル コンピューターまたはリモート コンピューター上の指定したキーを開きます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550967" data-raw-source="[&lt;strong&gt;SetupDiCreateDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550967)"><strong>SetupDiCreateDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイス インターフェイスのインスタンスに関する情報を格納するための不揮発性のレジストリ サブキーを作成し、キーへのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552075" data-raw-source="[&lt;strong&gt;SetupDiOpenDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552075)"><strong>SetupDiOpenDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイス インターフェイスのインスタンスに固有であり、キーへのハンドルを返しますの情報を格納するアプリケーションやドライバーで使用されるレジストリ サブキーを開きます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550986" data-raw-source="[&lt;strong&gt;SetupDiDeleteDeviceInterfaceRegKey&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550986)"><strong>SetupDiDeleteDeviceInterfaceRegKey</strong></a></p></td>
<td align="left"><p>デバイス インターフェイスのインスタンスに固有の情報を格納するアプリケーションやドライバーで使用されていたレジストリ サブキーを削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552169" data-raw-source="[&lt;strong&gt;SetupDiSetDeviceRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552169)"><strong>SetupDiSetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>指定したプラグ アンド プレイ デバイスのプロパティを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551967" data-raw-source="[&lt;strong&gt;SetupDiGetDeviceRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551967)"><strong>SetupDiGetDeviceRegistryProperty</strong></a></p></td>
<td align="left"><p>指定したプラグ アンド プレイ デバイスのプロパティを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551097" data-raw-source="[&lt;strong&gt;SetupDiGetClassRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551097)"><strong>SetupDiGetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>レジストリから指定したデバイス クラスのプロパティを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552135" data-raw-source="[&lt;strong&gt;SetupDiSetClassRegistryProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552135)"><strong>SetupDiSetClassRegistryProperty</strong></a></p></td>
<td align="left"><p>レジストリで指定されたデバイス クラスのプロパティを設定します。</p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551029" data-raw-source="[&lt;strong&gt;SetupDiGetActualModelsSection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551029)"><strong>SetupDiGetActualModelsSection</strong></a></p></td>
<td align="left"><p>適切な装飾を取得します<a href="inf-models-section.md" data-raw-source="[&lt;strong&gt;INF Models section&lt;/strong&gt;](inf-models-section.md)"> <strong>INF モデル セクション</strong></a>デバイス INF ファイルから、デバイスのインストール時に使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551039" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstall&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551039)"><strong>SetupDiGetActualSectionToInstall</strong></a></p></td>
<td align="left"><p>適切な取得<em>DDInstall</em>デバイス INF ファイルから、デバイスのインストール時に使用するセクション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551045" data-raw-source="[&lt;strong&gt;SetupDiGetActualSectionToInstallEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551045)"><strong>SetupDiGetActualSectionToInstallEx</strong></a></p></td>
<td align="left"><p>INF の名前を取得<em>DDInstall</em>セクションの指定したオペレーティング システムとプロセッサのアーキテクチャのデバイスをインストールします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551983" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551983)"><strong>SetupDiGetHwProfileFriendlyName</strong></a></p></td>
<td align="left"><p>ハードウェア プロファイルの ID に関連付けられているフレンドリ名を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551989" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileFriendlyNameEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551989)"><strong>SetupDiGetHwProfileFriendlyNameEx</strong></a></p></td>
<td align="left"><p>ローカルまたはリモート コンピューター上のハードウェア プロファイル ID に関連付けられているフレンドリ名を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551997" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551997)"><strong>SetupDiGetHwProfileList</strong></a></p></td>
<td align="left"><p>すべての現在定義されているハードウェア プロファイルの Id の一覧を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552006" data-raw-source="[&lt;strong&gt;SetupDiGetHwProfileListEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552006)"><strong>SetupDiGetHwProfileListEx</strong></a></p></td>
<td align="left"><p>ローカルまたはリモート コンピューター上のすべての現在定義されているハードウェア プロファイル Id の一覧を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff552104" data-raw-source="[&lt;strong&gt;SetupDiRestartDevices&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552104)"><strong>SetupDiRestartDevices</strong></a></p></td>
<td align="left"><p>指定されたデバイスを再起動または、必要に応じて、指定されたデバイスとして同じ関数とフィルター ドライバーによって運用されているすべてのデバイスを起動します。</p></td>
</tr>
</tbody>
</table>

 

 

 





