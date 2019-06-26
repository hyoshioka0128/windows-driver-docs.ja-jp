---
title: DIF_PROPERTYCHANGE
description: DIF_PROPERTYCHANGE
ms.assetid: 62f3380d-8cd1-4f4c-a727-1285de081b9e
keywords:
- DIF_PROPERTYCHANGE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_PROPERTYCHANGE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8bc4a6c5168cd2cb38f37798094d6cca04af2f48
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386900"
---
# <a name="difpropertychange"></a>DIF_PROPERTYCHANGE


DIF_PROPERTYCHANGE 要求は、デバイスのプロパティを変更することをインストーラーに通知します。 デバイスがされている有効、無効、開始、停止すると、または [プロパティ] ページには、いくつか項目が変更されました。 この差分要求では、インストーラーに、変更に参加する機会が与えられます。

### <a name="when-sent"></a>送信時

再起動、停止すると、デバイスがされている有効な場合、無効になっている、またはそのプロパティが変更されています。

プロパティ ページのプロバイダー DI_FLAGSEX_PROPCHANGE_PENDING フラグを設定するときに、Windows がこの要求を送信するなど、 **FlagsEx**のフィールド、 [ **SP_DEVINSTALL_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)デバイスの構造体。

デバイスを初めて開始時または後で再開を検出する方法の詳細については、インストーラーの操作」セクションを参照してください。

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
識別するハンドルを提供、[デバイス情報設定されている](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)デバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセットでのデバイスの構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_PROPCHANGE_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_propchange_params)構造が関連付けられている、 *DeviceInfoData*します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="none"></a>[なし]  

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、次を参照してください。[既定 DIF コード ハンドラーを呼び出す](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)します。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiChangeState**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)

### <a name="installer-operation"></a>インストーラーの操作

DIF_PROPERTYCHANGE 要求への応答では、インストーラーは、プロパティを変更する操作に参加できます。 クラスのインストール パラメーター (SP_PROPCHANGE_PARAMS) は、どの変更が行わを示します。

プロパティの変更には、システムの再起動が必要です。 システムを再起動する方法については、次を参照してください。 [ **SetupDiCallClassInstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)します。

Windows では、最初にデバイスをインストールする DIF_INSTALLDEVICE 要求を送信するときに、Windows はデバイスを開始されますが、インストールの一部として DIF_PROPERTYCHANGE 要求を送信しません。 インストーラーまたは共同インストーラーが最初にデバイスを起動する DIF_INSTALLDEVICE 要求を処理する必要がありますと、デバイスが、その後に再起動されるたびに、最初にデバイスが開始されると、カスタム インストール操作を実行する必要がある場合状態の変更操作は、デバイスが起動されていることが示す DIF_PROPERTYCHANGE 要求。

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


[**SetupDiChangeState**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdichangestate)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

[**SP_PROPCHANGE_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_propchange_params)

 

 






