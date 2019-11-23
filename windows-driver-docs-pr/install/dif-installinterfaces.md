---
title: DIF_INSTALLINTERFACES
description: DIF_INSTALLINTERFACES
ms.assetid: fd3eb56b-f73e-4699-accf-6bf70e2e54f8
keywords:
- デバイスとドライバーのインストールの DIF_INSTALLINTERFACES
topic_type:
- apiref
api_name:
- DIF_INSTALLINTERFACES
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 46ddce1bc4ddd6cf09a868538b546ccf424b80c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828825"
---
# <a name="dif_installinterfaces"></a>DIF_INSTALLINTERFACES


DIF_INSTALLINTERFACES 要求では、インストーラーはデバイスのデバイスインターフェイスの登録に参加できます。

### <a name="when-sent"></a>送信時

デバイスの共同インストーラーを登録した後、デバイスのインストールを完了する前。

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
デバイスを含む[デバイス情報セット](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)へのハンドルを提供します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
デバイス情報セット内のデバイスを識別する[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)構造体へのポインターを提供します。

<a href="" id="device-installation-parameters-"></a>デバイスのインストールパラメーター   
*Deviceinfodata*には、デバイスインストールパラメーター ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) が関連付けられています。

<a href="" id="class-installation-parameters"></a>クラスのインストールパラメーター  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストールパラメーター  
インストーラーによってデバイスのインストールパラメーターが変更される場合がありますが、通常はこの差分要求では変更されません。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーは、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラーコードを返すことができます。

クラスインストーラーがこの要求を正常に処理し、 [**Setupdicallclassinstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)がその後既定のハンドラーを呼び出す必要がある場合、クラスインストーラーは ERROR_DI_DO_DEFAULT を返します。

クラスインストーラーが、既定のハンドラーを直接呼び出すなど、この要求を正常に処理した場合、クラスインストーラーは NO_ERROR を返す必要があります。また、 **Setupdicallclassinstaller**は、その後、既定のハンドラーを再度呼び出すことはありません。

クラスインストーラーでは既定のハンドラーを直接呼び出すことができますが、クラスインストーラーでは既定のハンドラーの操作を置き換えないようにする必要**が  ます**。

 

既定のハンドラーの呼び出しの詳細については、「[既定の差分コードハンドラーの呼び出し](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)」を参照してください。

クラスインストーラーでエラーが発生した場合、インストーラーは適切な Win32 エラーコードを返す必要があります。また、 **Setupdicallclassinstaller**は、その後、既定のハンドラーを呼び出しません。

### <a name="default-dif-code-handler"></a>既定の差分コードハンドラー

[**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)

### <a name="installer-operation"></a>インストーラーの操作

DIF_INSTALLINTERFACES 要求に応答して、インストーラーは、インターフェイスを INF ファイルから登録するのではなく、プログラムによってデバイスインターフェイスを登録する場合があります。 通常、ベンダーから提供されたインストーラーは、この差分要求を処理しません。

DI_NOFILECOPY フラグが設定されていない限り、この差分要求を処理するインストーラーは、デバイスインターフェイスに必要なファイルをコピーする必要があります。

DI_NOFILECOPY フラグがクリアされていても、DI_NOVCP フラグが設定されている場合、インストーラーは、指定されたファイルキューにファイル操作をエンキューする必要がありますが、キューをコミットすることはできません。

インストーラーがデバイスインターフェイスを登録する場合、デバイスのカーネルモードコンポーネント (ドライバーなど) は[**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出して、インターフェイスを有効にする必要があります。

インストーラーが Win32 エラーコードを返すと、Windows によってインストールが停止されます。

差分コードの詳細については、「[差分コードの処理](https://docs.microsoft.com/windows-hardware/drivers/install/handling-dif-codes)」を参照してください。

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


[**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






