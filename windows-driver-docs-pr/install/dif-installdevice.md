---
title: DIF_INSTALLDEVICE
description: DIF_INSTALLDEVICE
ms.assetid: 2d369086-c2b6-45a4-a87e-51ff5725938f
keywords:
- DIF_INSTALLDEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_INSTALLDEVICE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d4229684528d2c527dd0567adfef96506f13b93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387054"
---
# <a name="difinstalldevice"></a>DIF_INSTALLDEVICE


DIF_INSTALLDEVICE 要求は、デバイスをインストールした後または前に、のタスクを実行するインストーラーを許可します。

### <a name="when-sent"></a>送信時

ドライバーを選択した後、デバイスの共同インストーラーを登録して、任意のデバイスの登録がインターフェイスです。

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
<td align="left"><p>処理できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クラスのインストーラー</p></td>
<td align="left"><p>処理できます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>インストーラーの入力

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
識別するハンドルを提供、[デバイス情報設定されている](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)格納しているデバイスをインストールします。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセットでのデバイスの構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでのデバイスのインストール パラメーターを変更できます、 *DeviceInfoData*します。 たとえば、インストーラーは DI_NEEDREBOOT フラグを設定可能性があります。 または、Windows が、新しくインストールされたドライバーと設定を動的にデバイスをオンラインにすることを防ぐために DI_DONOTCALLCONFIGMG フラグを設定、可能性があります。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーは、通常、NO_ERROR または ERROR_DI_POSTPROCESSING_REQUIRED を返します。 共同インストーラーは、Win32 エラー コードを返すも可能性があります。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。 既定の差分コード ハンドラーを呼び出す方法の詳細については、次を参照してください。[既定 DIF コード ハンドラーを呼び出す](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)します。

 

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)

### <a name="installer-operation"></a>インストーラーの操作

DIF_INSTALLDEVICE 要求への応答で、インストーラーでは、既定のハンドラーは、デバイスをインストールする前に、最終インストール操作が通常実行します。 たとえば、インストーラーは、チェックして、可能性がある変更、上位フィルター ドライバーと、レジストリに記載されているデバイスの低いフィルター ドライバー。

DI_NOFILECOPY フラグが設定されて、デバイスのインストール パラメータでない限り、この差分要求を処理するインストーラーは、ドライバー ファイル、コントロール パネルのファイルなど、デバイスに必要なファイルをコピーする必要があります。

DI_NOFILECOPY フラグがオフ、DI_NOVCP フラグが設定されている場合、インストーラーはファイル操作を指定したファイルのキューにエンキューする必要がありますが、キューにコミットする必要があります。

共同インストーラーには、前処理のパスで、または処理後のパスでは、この差分要求を処理できます。 前処理のパスでは、共同インストーラーは、Windows はドライバーをロードし、デバイスを起動する前に行う必要のあるすべての操作を実行します。

処理後のパスで、デバイスが稼働している DI_NEEDREBOOT フラグが設定された場合を除き、します。 このフラグが設定されている場合 Windows だったことはありません、デバイスがオンラインに動的にします。

インストーラーでは、Win32 エラー コードが返された場合、Windows は、インストールを破棄します。

インストールするために DIF_INSTALLDEVICE 送信 Windows では、新しいデバイスに対して、INF ファイルで特定できない場合、 *null ドライバー*します。 既定のハンドラー (**SetupDiInstallDevice**か、非 PnP デバイス (によって報告された[ **IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioreportdetecteddevice))、後者の場合、Windows インストール用のドライバーを nullデバイスです。

この試行が失敗した場合は、Windows の送信 DIF_INSTALLDEVICE もう一度、DI_FLAGSEX_SETFAILEDINSTALL フラグでは、この時点で設定、 [ **SP_DEVINSTALL_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)構造体。 ここでは、既定のハンドラーだけ FAILEDINSTALL 内フラグを設定、デバイスの**ConfigFlags**レジストリ値。 DI_FLAGSEX_SETFAILEDINSTALL フラグが設定されている場合は、クラスのインストーラーは NO_ERROR を返す必要があります。 または ERROR_DI_DO_DEFAULT と共同インストーラーには NO_ERROR を返す必要があります。

差分のコードの詳細については、次を参照してください。 [DIF コードの処理](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)します。

### <a name="calling-the-default-handler-setupdiinstalldevice"></a>**既定のハンドラー SetupDiInstallDevice を呼び出す**

呼び出すタイミングと方法に関する一般的な情報を**SetupDiInstallDevice**を参照してください[既定 DIF コード ハンドラーを呼び出す](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)します。

クラスのインストーラーがする必要があります操作をすべて実行まれな状況で**SetupDiInstallDevice**以降のデバイスを除く、操作が完了すると、クラスのインストーラーにする必要があります。

1.  操作を呼び出す前に行う必要がある実行**SetupDiInstallDevice**します。

2.  SP_DEVINSTALL_PARAMS DI_DONOTCALLCONFIGMGR フラグを設定します。**フラグ**デバイスのメンバー。 このフラグが設定されている場合**SetupDiInstallDevice**デバイスの開始を除くすべての既定のインストール操作を実行します。

3.  呼び出す**SetupDiInstallDevice**デバイスの開始を除くすべての既定のインストール操作を実行します。

4.  以降のデバイスを除く、すべての既定インストール操作が完了した後に行う必要がある操作を実行します。

5.  呼び出す[ **SetupDiRestartDevices** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdirestartdevices)デバイスを起動します。

6.  NO_ERROR を返す場合は、クラスのインストーラーがインストール操作を正常に完了またはインストール操作が失敗した場合は、Win32 のエラーを返します。

<a name="requirements"></a>必要条件
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


[**DIF_INSTALLDEVICEFILES**](dif-installdevicefiles.md)

[**SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






