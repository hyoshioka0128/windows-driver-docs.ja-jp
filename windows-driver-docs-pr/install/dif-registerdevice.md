---
title: DIF_REGISTERDEVICE
description: DIF_REGISTERDEVICE
ms.assetid: cb5f12f4-d429-4f02-b560-08807ffa3793
keywords:
- DIF_REGISTERDEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_REGISTERDEVICE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0e7c659ae9263048f0e964cc8897af235e6efb4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386897"
---
# <a name="difregisterdevice"></a>DIF_REGISTERDEVICE


DIF_REGISTERDEVICE 要求は、PnP マネージャーで、インスタンスを新しく作成したデバイスの登録に参加するインストーラーを使用します。 Windows では、非 PnP デバイスの場合は、この差分要求を送信します。

### <a name="when-sent"></a>送信時

インストーラーで予期せぬのデバイスへの応答を報告すると、 [ **DIF_DETECT** ](dif-detect.md)要求。 Windows では、デバイスのインストール前に、ハードウェアの追加ウィザードの分析フェーズでこの差分要求が送信されます。 また、Windows は、非 PnP の検出時にこの要求を送信します。

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
識別するハンドルを提供、[デバイス情報設定されている](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)デバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters-"></a>インストール パラメーターをクラスします。   
なし

### <a name="installer-output"></a>インストーラーの出力

なし

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR または Win32 エラー コードを返すことができます。 共同インストーラーは、この差分要求 ERROR_DI_POSTPROCESSING_REQUIRED を返しませんする必要があります。

インストーラーのデバイスに複製されていると判断した場合は、ERROR_DUPLICATE_FOUND を返します。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、次を参照してください。[既定 DIF コード ハンドラーを呼び出す](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)します。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

インストーラーでは、デバイスに重複していることを判断した場合、インストーラーは ERROR_DUPLICATE_FOUND を返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)

### <a name="installer-operation"></a>インストーラーの操作

A*デバイス インストール アプリケーション*通常マネージャー、PnP と非 PnP デバイスを登録するには、この差分要求を送信します。 Microsoft Windows 2000 以降、非 PnP デバイス登録する必要ありますをインストールする前にします。

インストーラーは、通常、重複データ検出を実行するには、この差分要求を処理します。 このようなインストーラーは、通常、既定のハンドラーを呼び出します ([**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)) し、検出ルーチンを指定します。 登録が成功し、インストーラーは、デバイスが重複しているではありませんを決定します。 インストーラーは NO_ERROR を返します。

共同インストーラーには、前処理のパスでは、この差分要求を処理するために操作を実行する必要があります。 後処理共同インストーラーが呼び出されるは、デバイス インスタンスはクラスのインストーラーまたは既定のハンドラーのいずれかによって既に登録されています。

インストーラーでは、この差分コードのエラーが返された場合通常 ERROR_DUPLICATE_FOUND、Windows デバイスを削除、デバイス情報のセットから。

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


[**DIF_DETECT**](dif-detect.md)

[**SetupDiRegisterDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregisterdeviceinfo)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






