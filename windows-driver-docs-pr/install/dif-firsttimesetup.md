---
title: DIF_FIRSTTIMESETUP
description: DIF_FIRSTTIMESETUP
ms.assetid: 6ac4da58-3f4f-4fcd-96e2-c480975159e0
keywords:
- DIF_FIRSTTIMESETUP デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_FIRSTTIMESETUP
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 351cc3ee4fda06893f835b389b6a643c2d35f8e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386904"
---
# <a name="diffirsttimesetup"></a>DIF_FIRSTTIMESETUP


この差分コードは、システムの使用に予約されています。 ベンダーから提供されたインストーラーは、仕入先がインストーラーで検出する必要がありますが、非 PnP デバイスを提供しない限り、この要求を処理する必要があります。

DIF_FIRSTTIMESETUP 要求は、オペレーティング システムの初期インストール時に完了する必要がある任意のクラスに固有のインストール タスクを実行するインストーラーを指示します。

### <a name="when-sent"></a>送信時

フル インストール モードのセットアップ。

### <a name="who-handles"></a>処理します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>クラスの共同インストーラー</p></td>
<td align="left"><p>処理できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>デバイスの共同インストーラー</p></td>
<td align="left"><p>処理しません</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クラスのインストーラー</p></td>
<td align="left"><p>処理できます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>インストーラーの入力

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
装置のデバイス情報へのハンドルを設定します。 [デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)に関連付けられている、 *DeviceInfoSet*します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
なし

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoSet*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
インストーラーにデバイス情報要素を追加する、 *DeviceInfoSet*がインストールされているデバイスが検出された各の。 インストーラーは、グローバル クラス ドライバー一覧を作成も可能性があります。

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでのデバイスのインストール パラメーターを変更できます、 *DeviceInfoSet*または新しいデバイス情報の要素が作成されます。

### <a name="installer-return-value"></a>インストーラーの戻り値

クラスの共同インストーラーは、前処理または後処理中にデバイスを検出できます。 このような共同インストーラーは ERROR_DI_POSTPROCESSING_REQUIRED (処理後) を返します。 または、検出操作後に NO_ERROR または Win32 エラー コードを返します。 共同インストーラーから、デバイスが検出されない場合は、前処理のパスから NO_ERROR を返します。

クラスのインストーラーは、デバイスが検出される場合、インストーラーは NO_ERROR または適切な Win32 エラー コードを返します。 クラスのインストーラーがこの差分要求を処理しない場合、インストーラーは ERROR_DI_DO_DEFAULT を返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

フル インストール モードのセットアップ時に非 PnP デバイスを検出するためには、インストーラーは DIF_FIRSTTIMESETUP 要求を処理する必要があります。 フル インストール モードのセットアップを送信しません、 [ **DIF_DETECT** ](dif-detect.md)インストーラーに要求します。

フル インストール モードのセットアップは、空の DIF_FIRSTTIMESETUP 要求を送信*DeviceInfoSet*します。 インストーラーは非 PnP デバイスのレガシの検出を実行することができますに追加することと、 *DeviceInfoSet*します。 Windows 9 からレガシ デバイスのインストールを移行する場合、システム提供のインストーラーはこの差分要求を処理もできる x/自分または Microsoft Windows 2000 以降のバージョンの Windows を Windows NT です。

インストーラーは、カーネル モードの検出のコンポーネントを呼び出すことによって、またはを参照して、レジストリの情報に基づいて、そのセットアップ クラスの新しいデバイスを検出*unattend.txt*移行中に DLL が実行時に格納されている情報、オペレーティング システムをアップグレードします。

次のように、デバイスのドライバーを選択する必要があります、インストーラーに、インストーラーは、非 PnP デバイスが検出される場合: デバイス情報の要素の作成 ([**SetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa))、設定、SPDRP_HARDWAREIDプロパティを呼び出して[ **SetupDiSetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)、呼び出す[ **SetupDiBuildDriverInfoList**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)、しを呼び出します[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)を送信する、 [ **DIF_SELECTBESTCOMPATDRV** ](dif-selectbestcompatdrv.md)要求。

1 つまたは複数のインストーラーは、この差分コードへの応答でデバイスを検出、フル インストール モードのセットアップは、デバイスをインストールしようとします。 フル インストール モードのセットアップは、一覧内のすべてのデバイスをインストールしようとしていますインストーラーは、以前に構成されたデバイスを返す場合、フル インストール モードのセットアップは、デバイスを 2 回インストールされます。

インストーラーでは、サイレント モードでこの差分要求を処理する必要があります。 これは、ユーザーに UI を表示することがなく。

インストーラーでは、コンピューターの再起動を必要とするこの差分要求を処理するときに、タスクは実行しないでください。 たとえば、クラスのインストーラーでは、どのドライバーが、再起動後に成功を決定するための次回起動時に読み込むドライバーは設定しないでください。

フル インストール モードのセットアップ時に非 PnP デバイスを検出するために、インストーラーは、この要求を処理する必要があります。 フル インストール モードのセットアップでは、DIF_DETECT 要求を送信しません。

差分のコードの詳細については、次を参照してください。 [DIF コードの処理](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Microsoft Windows 2000 以降のバージョンの Windows でサポートされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h (Setupapi.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DIF_SELECTBESTCOMPATDRV**](dif-selectbestcompatdrv.md)

[**SetupDiBuildDriverInfoList**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdibuilddriverinfolist)

[**SetupDiCallClassInstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)

[**SetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)

[**SetupDiSetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






