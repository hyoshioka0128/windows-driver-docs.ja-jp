---
title: DIF_INSTALLDEVICE
description: DIF_INSTALLDEVICE
ms.assetid: 2d369086-c2b6-45a4-a87e-51ff5725938f
keywords:
- デバイスとドライバーのインストールの DIF_INSTALLDEVICE
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
ms.openlocfilehash: 285238b8e27db90db58c2bba3169a81c763c6eca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828852"
---
# <a name="dif_installdevice"></a>DIF_INSTALLDEVICE


DIF_INSTALLDEVICE 要求を使用すると、デバイスのインストールの前または後に、インストーラーでタスクを実行できます。

### <a name="when-sent"></a>送信時

ドライバーを選択し、デバイスの共同インストーラーを登録して、デバイスインターフェイスを登録します。

### <a name="who-handles"></a>処理対象

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>クラスの共同インストーラー</p></td>
<td align="left"><p>処理可能</p></td>
</tr>
<tr class="even">
<td align="left"><p>デバイスの共同インストーラー</p></td>
<td align="left"><p>処理可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クラスインストーラー</p></td>
<td align="left"><p>処理可能</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>インストーラーの入力

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
インストールするデバイスを含む[デバイス情報セット](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)へのハンドルを提供します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
デバイス情報セット内のデバイスの[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)構造体へのポインターを提供します。

<a href="" id="device-installation-parameters-"></a>デバイスのインストールパラメーター   
*Deviceinfodata*には、デバイスインストールパラメーター ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) が関連付けられています。

<a href="" id="class-installation-parameters"></a>クラスのインストールパラメーター  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストールパラメーター  
インストーラーでは、 *Deviceinfodata*のデバイスインストールパラメーターを変更できます。 たとえば、インストーラーで DI_NEEDREBOOT フラグを設定したり、DI_DONOTCALLCONFIGMG フラグを設定して、新しくインストールされたドライバーと設定を使用してデバイスを動的にオンラインにしないようにすることができます。

### <a name="installer-return-value"></a>インストーラーの戻り値

通常、共同インストーラーは NO_ERROR または ERROR_DI_POSTPROCESSING_REQUIRED を返します。 また、共同インストーラーも Win32 エラーコードを返す場合があります。

クラスインストーラーがこの要求を正常に処理し、 [**Setupdicallclassinstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)がその後既定のハンドラーを呼び出す必要がある場合、クラスインストーラーは ERROR_DI_DO_DEFAULT を返します。

クラスインストーラーが、既定のハンドラーを直接呼び出すなど、この要求を正常に処理した場合、クラスインストーラーは NO_ERROR を返す必要があります。また、 **Setupdicallclassinstaller**は、その後、既定のハンドラーを再度呼び出すことはありません。

クラスインストーラーでは既定のハンドラーを直接呼び出すことができますが、クラスインストーラーでは既定のハンドラーの操作を置き換えないようにする必要**が   ます**。 既定の差分コードハンドラーを呼び出す方法の詳細については、「[既定の差分コードハンドラーの呼び出し](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)」を参照してください。

 

クラスインストーラーでエラーが発生した場合、インストーラーは適切な Win32 エラーコードを返す必要があります。また、 **Setupdicallclassinstaller**は、その後、既定のハンドラーを呼び出しません。

### <a name="default-dif-code-handler"></a>既定の差分コードハンドラー

[**SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)

### <a name="installer-operation"></a>インストーラーの操作

DIF_INSTALLDEVICE 要求に応答して、インストーラーは通常、既定のハンドラーがデバイスをインストールする前に最終的なインストール操作を実行します。 たとえば、インストーラーは、レジストリに一覧表示されているデバイスの上位フィルタードライバーと下位フィルタードライバーを確認し、変更する場合があります。

デバイスのインストールパラメーターに DI_NOFILECOPY フラグが設定されていない限り、この差分要求を処理するインストーラーは、ドライバーファイルやコントロールパネルファイルなど、デバイスに必要なファイルをコピーする必要があります。

DI_NOFILECOPY フラグがクリアされていても、DI_NOVCP フラグが設定されている場合、インストーラーは、指定されたファイルキューにファイル操作をエンキューする必要がありますが、キューをコミットすることはできません。

共同インストーラーは、そのプリプロセスパスまたはその後処理パスで、この差分要求を処理できます。 前処理パスでは、共同インストーラーは、Windows がドライバーを読み込み、デバイスを起動する前に実行する必要があるすべての操作を実行します。

その後処理パスでは、DI_NEEDREBOOT フラグが設定されていない限り、デバイスは稼働しています。 このフラグが設定されている場合、Windows はデバイスを動的にオンラインにできませんでした。

インストーラーが Win32 エラーコードを返した場合、Windows はインストールを破棄します。

新しいデバイスの INF ファイルが見つからない場合は、 *null ドライバー*をインストールしようとすると DIF_INSTALLDEVICE が送信されます。 既定のハンドラー (**Setupdiinstalldevice**またはは、 [**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)によって報告された非 PnP デバイス) です。後者の場合、Windows はデバイス用に null ドライバーをインストールします。

この試行が失敗した場合は、Windows によって DIF_INSTALLDEVICE が再び送信されます。このとき、 [**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)構造体に DI_FLAGSEX_SETFAILEDINSTALL フラグが設定されています。 この場合、既定のハンドラーは、デバイスの**configflags**レジストリ値に、失敗したインストールフラグだけを設定します。 DI_FLAGSEX_SETFAILEDINSTALL フラグが設定されている場合、クラスインストーラーは NO_ERROR または ERROR_DI_DO_DEFAULT を返す必要があり、共同インストーラーは NO_ERROR を返す必要があります。

差分コードの詳細については、「[差分コードの処理](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)」を参照してください。

### <a name="calling-the-default-handler-setupdiinstalldevice"></a>**既定のハンドラー SetupDiInstallDevice を呼び出しています**

**Setupdiinstalldevice**を呼び出すタイミングと方法に関する一般的な情報については、「[既定の差分コードハンドラーの呼び出し](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)」を参照してください。

デバイスの開始を除き、すべての**Setupdiinstalldevice**操作が完了した後に、クラスインストーラーが操作を実行することが必要なまれな状況では、クラスインストーラーは次のことを行う必要があります。

1.  **Setupdiinstalldevice**を呼び出す前に実行する必要がある操作を実行します。

2.  SP_DEVINSTALL_PARAMS で DI_DONOTCALLCONFIGMGR フラグを設定します。デバイスの**フラグ**メンバー。 このフラグが設定されている場合、 **Setupdiinstalldevice**は、デバイスを起動する場合を除き、既定のインストール操作をすべて実行します。

3.  **Setupdiinstalldevice**を呼び出して、デバイスの起動以外のすべての既定のインストール操作を実行します。

4.  デバイスの起動以外のすべての既定のインストール操作が完了した後に実行する必要がある操作を実行します。

5.  [**SetupDiRestartDevices**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdirestartdevices)を呼び出して、デバイスを起動します。

6.  クラスインストーラーによってインストール操作が正常に完了したか、インストール操作が失敗した場合に Win32 エラーが返された場合は、NO_ERROR を返します。

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
<td align="left">Setupapi.log (Setupapi.log を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DIF_INSTALLDEVICEFILES**](dif-installdevicefiles.md)

[**SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






