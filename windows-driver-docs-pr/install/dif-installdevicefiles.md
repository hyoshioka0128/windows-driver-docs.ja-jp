---
title: DIF_INSTALLDEVICEFILES
description: DIF_INSTALLDEVICEFILES
ms.assetid: 544a9a88-156e-494d-9ef0-8070addfa86b
keywords:
- DIF_INSTALLDEVICEFILES デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_INSTALLDEVICEFILES
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1f8841725e55efe62b2c6317be5c62cbecea1c32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387051"
---
# <a name="difinstalldevicefiles"></a>DIF_INSTALLDEVICEFILES


DIF_INSTALLDEVICEFILES 要求は、デバイスをサポートする、またはデバイスのファイルの一覧を作成するファイルのコピーに参加するインストーラーを許可します。 デバイス ファイルには、選択したドライバー、任意のデバイスのインターフェイスと、共同インストーラーのファイルが含まれます。

### <a name="when-sent"></a>送信時

[システム指定のデバイスのインストール コンポーネント](https://docs.microsoft.com/windows-hardware/drivers/install/system-provided-device-installation-components)さまざまな理由は、この差分要求を送信します。 一部のデバイス インストールのコンポーネントでは、インストールを続行する前に、関連するすべてのファイルをコピーできることを確認するには、DIF_REGISTER_COINSTALLERS、DIF_INSTALLINTERFACES、および DIF_INSTALL_DEVICE する前にこの差分要求を送信します。 デバイス インストールの一部のコンポーネントは、この差分要求を省略し、これら 3 つの差分要求の処理中にコピーするファイルを期待します。 さらに、一部のデバイスのインストール コンポーネントは、デバイスに関連付けられているファイルの一覧を取得するには、この差分要求を送信します。

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
識別するハンドルを提供、[デバイス情報設定されている](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)デバイスのサポート ファイルのコピーを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoData*します。

DI_NOVCP フラグが設定されている場合、デバイスのインストール パラメータを含む、有効な**FileQueue**ハンドルと、この差分要求を処理するためのインストーラーは、このキューにそのファイルの操作を追加し、キューをコミットしないでください。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
インストーラーを変更できる、 **FileQueue**いずれかを使用する必要がある場合、します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、次を参照してください。[既定 DIF コード ハンドラーを呼び出す](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)します。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiInstallDriverFiles**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)

### <a name="installer-operation"></a>インストーラーの操作

DIF_INSTALLDEVICEFILES への応答では、要求、インストーラーは、すべての必要なファイル操作を指定します。 たとえば、インストーラーは、デバイスのインストールに必要なコピーする追加ファイルを指定できます。 インストーラーでファイルの操作を指定しますに追加して DI_NOVCP フラグが設定されている場合、 **FileQueue**デバイス インストールのパラメーターにします。 など、ファイル キューの機能を Microsoft Windows SDK ファイルのキューを使用する方法については、リファレンス ページを参照してください**SetupInstallFilesFromInfSection**します。

デバイスのインストール中にこの差分要求が送信され、インストーラーは、Microsoft Win32 エラー コードを返します、Windows は、インストールを停止します。

場合、[システム指定のデバイスのインストール コンポーネント](https://docs.microsoft.com/windows-hardware/drivers/install/system-provided-device-installation-components)をデバイスに関連付けられたファイルの一覧を取得するこの差分要求を送信、コンポーネントのファイルのキューを取得しますが、キューをコミットしません。

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


[**SetupDiInstallDriverFiles**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldriverfiles)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






