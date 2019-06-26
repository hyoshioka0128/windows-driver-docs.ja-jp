---
title: DIF_ALLOW_INSTALL
description: DIF_ALLOW_INSTALL
ms.assetid: 0bcda90e-f9f1-4965-a08b-d884077a2e8b
keywords:
- DIF_ALLOW_INSTALL デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_ALLOW_INSTALL
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b891cfe32185e853af382f0d7a5f47fa729a7cca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373503"
---
# <a name="difallowinstall"></a>DIF_ALLOW_INSTALL


DIF_ALLOW_INSTALL 要求は、Windows デバイスのインストールを続行するかどうか、デバイスのインストーラーを確認します。

### <a name="when-sent"></a>送信時

後、デバイスがデバイスをインストールする前にドライバーを選択します。

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
<td align="left"><p>処理しないでください。</p></td>
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
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="none"></a>[なし]  

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR または Win32 エラーを返すことができます。 共同インストーラーは、この差分要求 ERROR_DI_POSTPROCESSING_REQUIRED を返しませんする必要があります。

クラスのインストーラーは、通常、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

この差分要求の標準的な Win32 のエラー コード、ERROR_DI_DONT_INSTALL ERROR_NON_WINDOWS_NT_DRIVER があります。

**注**  クラスのインストーラーと共同インストーラーが、freturn ERROR_REQUIRES_INTERACTIVE_WINDOWSTATION いないデバイスのインストールが失敗する原因となったためです。 クラスのインストーラーと共同インストーラーをサポートする必要があります、デバイスのインストールは、ユーザーの介入を必要とする場合、[完了-インストール アクション](https://docs.microsoft.com/windows-hardware/drivers/install/finish-install-actions--windows-vista-and-later-)します。

 

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

DIF_ALLOW_INSTALL 要求への応答では、インストーラーは、Windows がデバイスをインストールできるかどうかを確認します。

インストーラーが (たとえば、ドライバーが Windows 9 x 専用ドライバー NT ベースのオペレーティング システムで正しく動作しないことである場合) には、選択したドライバーが正しくないことを判断した場合、またはバグが存在する、選択したドライバーが既知であると判断した場合、この要求が失敗することができます。

インストーラーが DI_QUIETINSTALL フラグがデバイスのインストール パラメーターで設定され、インストーラーにはデバイスのインストール中に UI を表示する場合、この要求が失敗する可能性があります。 ただし、インストーラーがある DIF_NEWDEVICEWIZARD_FINISHINSTALL 要求への応答の UI ページを通常提供ためには、このエラーはまれです。 その場合は、UI は、/quiet フラグが設定されている DIF_ALLOW_INSTALL 要求を指すからインストーラーを妨げません。 ただし、インストーラーは、完了-インストールの場合にその UI を制限ことはできない場合、DI_QUIETINSTALL フラグが設定されている場合、インストーラーはこの差分要求失敗する必要があります。 UI を表示するベンダーから提供されたコードを呼び出す場合、インストーラーは、この制限をなどのがあります。

インストーラーには、この差分要求が失敗した場合、Windows は、インストールを停止します。

インストーラーには、この差分要求が失敗した DI_QUIETINSTALL がデバイスのインストール パラメーターで設定されていない場合は、インストーラーはデバイスがないインストールされている理由を説明するメッセージとダイアログ ボックスを表示する必要があります。

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


[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






