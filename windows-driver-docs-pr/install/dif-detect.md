---
title: DIF_DETECT
description: DIF_DETECT
ms.assetid: 866a99fc-f48e-447d-b5eb-6339dc98d3f2
keywords:
- DIF_DETECT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_DETECT
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a26c57dd7f444ad87f49240f4b73a1a4f2d33594
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354657"
---
# <a name="difdetect"></a>DIF_DETECT


DIF_DETECT 要求は、特定のクラスの非 PnP デバイスを検出し、デバイス情報のセットに、デバイスを追加するインストーラーを指示します。 この要求は、非 PnP デバイスで使用されます。

### <a name="when-sent"></a>送信時

ときに、**ハードウェアの追加ウィザード**非 PnP デバイスを検出します。

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
識別するハンドルを提供、[デバイス情報設定されている](https://docs.microsoft.com/windows-hardware/drivers/install/device-information-sets)します。 [デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)に関連付けられている、 *DeviceInfoSet*します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
なし

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
インストールのパラメーターに関連付けられているデバイスがある、 *DeviceInfoSet*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_DETECTDEVICE_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)構造が関連付けられている、 *DeviceInfoSet*します。 パラメーターには、クラスのインストーラーを検出操作の進行状況を示すために呼び出すコールバック ルーチンが含まれています。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
インストーラーにデバイス情報要素を追加する、 *DeviceInfoSet*デバイスごとに検出されると、デバイスが既に検出し、インストールされているかどうかに関係なく。

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでのデバイスのインストール パラメーターを変更できます、 *DeviceInfoSet*または新しいデバイス情報の要素が作成されます。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーから、デバイスが検出されない場合は、前処理のパスから NO_ERROR を返します。 共同インストーラーは、デバイスを検出、前処理または後処理中に、でき、NO_ERROR または Win32 エラー コードを返します。

クラスのインストーラーは、デバイスを検出、NO_ERROR または適切な Win32 エラー コードが返されます。 クラスのインストーラーがこの差分要求を処理しない場合は、ERROR_DI_DO_DEFAULT を返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

DIF_DETECT 要求に応答インストーラーは、セットアップ クラスのデバイスを検出できます。

インストーラーは、デバイスが検出される場合、次には少なくとも行う必要があります。

-   呼び出す、 **DetectProgressNotify**コールバック ルーチンで、 [ **SP_DETECTDEVICE_PARAMS** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)検出に著しいがかかる可能性がある場合は、インストールのパラメーターをクラス時間の長さ。

-   インストーラーが検出した各デバイスは、次のことを行う必要があります。
    -   デバイス情報の要素の作成 ([**SetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa))。
    -   ドライバーの選択の情報を提供します。

        インストーラーでは、デバイスのドライバーを手動で選択できますか、インストーラーは、Windows がデバイスに対して、INF を検索に使用する、デバイスのハードウェア ID を設定できます。 インストーラーは、呼び出すことによって、ハードウェア ID を設定[ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)で、*プロパティ*SPDRP_HARDWAREID の値。

    -   可能性があるいくつかのデバイスのインストール パラメーターを設定します。

-   正常な検出の NO_ERROR を返すまたは Win32 エラー コードを返します。

1 つまたは複数のインストーラーは、この差分コードへの応答内のデバイスを検出、Windows はデバイスの現在のリストに検出されたデバイスの一覧を比較します。 インストーラーでは、新しいデバイスを検出、Windows は、デバイスをインストールしようとします。 インストーラーは、セットアップのリストに表示されるデバイスを省略すると、Windows は通常、デバイスを削除します。

フル インストール モードのセットアップ時に非 PnP デバイスを検出するために、インストーラーを処理する必要があります、 [ **DIF_FIRSTTIMESETUP** ](dif-firsttimesetup.md)要求。 フル インストール モードのセットアップでは、インストーラーに DIF_DETECT 要求を送信しません。

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

[**DIF_FIRSTTIMESETUP**](dif-firsttimesetup.md)

[**SetupDiCreateDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfoa)

[**SP_DETECTDEVICE_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_detectdevice_params)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






