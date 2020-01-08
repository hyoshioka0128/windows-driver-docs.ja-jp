---
title: DIF_REMOVE
description: DIF_REMOVE
ms.assetid: 14429756-c059-46d7-bd1c-0ae57d1ec8b5
keywords:
- デバイスとドライバーのインストールの DIF_REMOVE
topic_type:
- apiref
api_name:
- DIF_REMOVE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fc772967ee59347bcfc5ce4163b2428e8dbee2e1
ms.sourcegitcommit: 9355a80229bb2384dd45493d36bdc783abdd8d7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694240"
---
# <a name="dif_remove"></a>DIF_REMOVE


DIF_REMOVE 要求によって、Windows がデバイスを削除しようとしていることがインストーラーに通知され、インストーラーに削除の準備をする機会が与えられます。

### <a name="when-sent"></a>送信時

ユーザーがデバイスマネージャーでデバイスを削除したとき。

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
削除するデバイスを含む[デバイス情報セット](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)へのハンドルを提供します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
デバイス情報セット内のデバイスの[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)構造体へのポインターを提供します。

<a href="" id="device-installation-parameters-"></a>デバイスのインストールパラメーター   
*Deviceinfodata*には、デバイスインストールパラメーター ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)) が関連付けられています。

<a href="" id="class-installation-parameters"></a>クラスのインストールパラメーター  
[**SP_REMOVEDEVICE_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_removedevice_params)構造体は、 *deviceinfodata*に関連付けられる場合があります。

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)で DI_CLASSINSTALLPARAMS フラグがクリアされている場合、要求のクラスインストールパラメーターはありません。 この場合、ハードウェアプロファイルが指定されていないため、デバイスはシステム全体から削除されます。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="none"></a>存在  

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーは、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラーコードを返すことができます。

クラスインストーラーがこの要求を正常に処理し、 [**Setupdicallclassinstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)がその後既定のハンドラーを呼び出す必要がある場合、クラスインストーラーは ERROR_DI_DO_DEFAULT を返します。

クラスインストーラーが、既定のハンドラーを直接呼び出すなど、この要求を正常に処理した場合、クラスインストーラーは NO_ERROR を返す必要があります。また、 **Setupdicallclassinstaller**は、その後、既定のハンドラーを再度呼び出すことはありません。

クラスインストーラーでは既定のハンドラーを直接呼び出すことができますが、クラスインストーラーでは既定のハンドラーの操作を置き換えないようにする必要**が   ます**。

 

既定のハンドラーの呼び出しの詳細については、「[既定の差分コードハンドラーの呼び出し](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)」を参照してください。

クラスインストーラーでエラーが発生した場合、インストーラーは適切な Win32 エラーコードを返す必要があります。また、 **Setupdicallclassinstaller**は、その後、既定のハンドラーを呼び出しません。

### <a name="default-dif-code-handler"></a>既定の差分コードハンドラー

[**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)

### <a name="installer-operation"></a>インストーラーの操作

DIF_REMOVE 要求に応答して、インストーラーは通常、いくつかのクリーンアップ操作を実行します。 この場合、共同インストーラーは NO_ERROR を返し、クラスインストーラーは ERROR_DI_DO_DEFAULT を返します。

インストーラーによってデバイスが削除されないと判断された場合、インストーラーは Win32 エラーコードを返すことによって差分要求を失敗させます。 DI_QUIETINSTALL フラグがオフの場合、インストーラーは、デバイスが削除されていない理由を説明するメッセージをユーザーに表示する必要があります。

共同インストーラーでは、 **Setupdiremovedevice**を呼び出すことによって、デバイス自体を削除することはできません。 共同インストーラーは、通常、デバイスが正常に削除された後に、後処理でこの要求を処理します。

たとえば、共同インストーラーでレジストリ内の情報を削除する必要がある場合、共同インストーラーは、前のインストーラーが削除要求を正常に完了した場合にのみ、後処理でそれを実行します。 そのプリプロセスパスでは、共同インストーラーがそのコンテキストパラメーターにレジストリ情報を格納し、ERROR_DI_POSTPROCESSING_REQUIRED を返して後処理を要求します。 Windows がこの差分要求の後処理のために共同インストーラーを呼び出す場合、共同インストーラーは、差分の状態が NO_ERROR ことを確認してから、レジストリ情報を削除する必要があります。 共同インストーラーによって前処理パスのレジストリ情報が削除され、クラスインストーラー (または別の共同インストーラー) によって DIF_REMOVE が失敗した場合、共同インストーラーによってデバイスが予期しない状態のままになることがあります。

インストーラーでは、ファイルが別のデバイスで使用されている場合に、この差分要求を処理するときにファイルを削除しないでください。

Windows は、PnP クエリを開始する前に、この差分要求を送信します。処理を削除および削除します。

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

## <a name="see-also"></a>「


[**SetupDiRemoveDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiremovedevice)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_devinstall_params_a)

[**SP_REMOVEDEVICE_PARAMS**](https://docs.microsoft.com/windows/win32/api/setupapi/ns-setupapi-sp_removedevice_params)

 

 






