---
title: DIF_INSTALLINTERFACES
description: DIF_INSTALLINTERFACES
ms.assetid: fd3eb56b-f73e-4699-accf-6bf70e2e54f8
keywords:
- DIF_INSTALLINTERFACES デバイスとドライバーのインストール
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
ms.openlocfilehash: a043d19fdcec80d16b2d29aceb423cb1e44ea88a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387045"
---
# <a name="difinstallinterfaces"></a>DIF_INSTALLINTERFACES


DIF_INSTALLINTERFACES 要求は、デバイスのインターフェイス、デバイスの登録に参加するインストーラーを許可します。

### <a name="when-sent"></a>送信時

デバイスの共同インストーラーを登録した後、デバイスのインストールを完了する前にします。

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
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーは、デバイスのインストール パラメータを変更可能性がありますが、通常はこの差分要求。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、次を参照してください。[既定 DIF コード ハンドラーを呼び出す](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)します。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)

### <a name="installer-operation"></a>インストーラーの操作

DIF_INSTALLINTERFACES への応答要求インストーラーは、INF ファイルで登録されているインターフェイスはなくプログラムによってデバイス インターフェイスを登録する可能性があります。 通常、ベンダーから提供されたインストーラーは、この差分要求を処理しません。

DI_NOFILECOPY フラグが設定されていない限り、この差分要求を処理するインストーラーはデバイス インターフェイスに必要なファイルをコピーする必要があります。

DI_NOFILECOPY フラグがオフ、DI_NOVCP フラグが設定されている場合、インストーラーはファイル操作を指定したファイルのキューにエンキューする必要がありますが、キューにコミットする必要があります。

インストーラーは、デバイス インターフェイスを登録場合、デバイス (たとえば、ドライバー) のカーネル モード コンポーネントを呼び出す必要があります[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)インターフェイスを有効にします。

インストーラーでは、Win32 エラー コードを返します、Windows は、インストールを停止します。

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


[**SetupDiInstallDeviceInterfaces**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldeviceinterfaces)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






