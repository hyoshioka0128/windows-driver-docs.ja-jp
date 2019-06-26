---
title: DIF_DESTROYPRIVATEDATA
description: DIF_DESTROYPRIVATEDATA
ms.assetid: 4f5d423d-52a5-4f7a-9847-b0e65b1c6f09
keywords:
- DIF_DESTROYPRIVATEDATA デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_DESTROYPRIVATEDATA
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: db2b92e746711ced56af442e369bb40fadc4e189
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354668"
---
# <a name="difdestroyprivatedata"></a>DIF_DESTROYPRIVATEDATA


DIF_DESTROYPRIVATEDATA 要求を任意のメモリまたはリソース割り当てられに格納されていることを解放するクラスのインストーラーの指示、 **ClassInstallReserved**のフィールド、 [ **SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)構造体。

### <a name="when-sent"></a>送信時

Windows を破棄すると、[デバイス情報設定されている](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)または[ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)要素、または Windows で共同インストーラーとデバイスのクラスのインストーラーのリストを破棄する場合。

### <a name="who-handles"></a>処理します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>クラスの共同インストーラー</p></td>
<td align="left"><p>処理しません</p></td>
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
装置のデバイス情報へのハンドルを設定します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
必要に応じてへのポインターを提供、 [ **SP_DEVINFO_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイスのインストール パラメーター ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)) に関連付けられている、 *DeviceInfoData*、指定した場合または、 *DeviceInfoSet*.

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
インストーラーをオフにできる、 **ClassInstallReserved**フィールドに、デバイスのインストール パラメータ ([**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a))。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーは、この差分要求を処理しません。 単に、前処理のパスで NO_ERROR を返します。

クラスのインストーラーは、通常、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

クラスのインストーラーは、メモリやリソースを解放 DIF_DESTROYPRIVATEDATA 要求に応答の 割り当てられに格納されていること、 **ClassInstallReserved**のフィールド、 [ **SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)構造体。

共同インストーラーを使用する必要があります、 **ClassInstallReserved**フィールド。

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

 

 






