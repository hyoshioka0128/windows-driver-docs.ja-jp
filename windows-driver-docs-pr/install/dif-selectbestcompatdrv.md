---
title: DIF_SELECTBESTCOMPATDRV
description: DIF_SELECTBESTCOMPATDRV
ms.assetid: aa10f39f-718b-4160-9cfa-668fb0349156
keywords:
- DIF_SELECTBESTCOMPATDRV デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_SELECTBESTCOMPATDRV
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d5dbddad81dd833e2411d12d55a06bc1ee60df4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386895"
---
# <a name="difselectbestcompatdrv"></a>DIF_SELECTBESTCOMPATDRV

> [!NOTE]
> この要求は、Windows 10 バージョン 1703 (レッドス トーン 2) で非推奨とされました。 最近のバージョンの Windows では、このコールバックは呼び出されません。

DIF_SELECTBESTCOMPATDRV 要求は、インストーラー、デバイス情報要素の互換性のあるドライバーの一覧から最適なドライバーを選択できます。

### <a name="when-sent"></a>送信時

オペレーティング システムが新しい PnP デバイスのインストールの準備中または PnP デバイス ドライバーの変更操作を実行する場合。

この差分要求は通常、PnP の構成時に使用されます。 デバイスは手動でインストールされている場合に、Windows が送信を[ **DIF_SELECTDEVICE** ](dif-selectdevice.md)要求。

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

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでは、デバイスのインストール パラメーターを変更できます。 ただし、通常そのときではなくこの差分の要求を処理します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
インストーラーに関連付けられているドライバーの一覧の変更時に、副作用として、 *DeviceInfoData*、具体的には、SP_DRVINSTALL_PARAMS します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、次を参照してください。[既定 DIF コード ハンドラーを呼び出す](https://docs.microsoft.com/windows-hardware/drivers/install/calling-the-default-dif-code-handlers)します。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiSelectBestCompatDrv**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)

### <a name="installer-operation"></a>インストーラーの操作

インストーラーでは、PnP デバイス用ドライバーを選択する際に参加するには、この差分要求を処理します。 インストーラーには、通常、次の方法のいずれかでこの差分要求に応答しています。

-   何もしない。

    インストーラーには、特別な選択の要件がなければ、この差分要求への応答には何もしません。 クラスのインストーラーは ERROR_DI_DO_DEFAULT を返し、共同インストーラーには NO_ERROR が返されます。

-   ドライバーの一覧に 1 つまたは複数のドライバーのパラメーターを変更します。

    たとえば、インストーラーは、DNF_BAD_DRIVER マークすることで、デバイスの考慮の対象からドライバーを削除可能性があります。 インストーラーでは、次の手順でドライバーのパラメーターを変更します。

    1.  呼び出すことによってリスト内の最初のドライバーに関する情報を取得[ **SetupDiEnumDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)と[ **SetupDiGetDriverInstallParams** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa). 必要に応じて、ドライバーのパラメーターを変更し、呼び出すことによって、変更を適用[ **SetupDiSetDriverInstallParams**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdriverinstallparamsa)します。

        ドライバーが最悪な選択肢である場合は、パラメーターを設定、ドライバーのランク 0 xffff を以上に、ドライバーのインストール。 参照してください[Windows ドライバーを選択する方法](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-selects-drivers)詳細についてはします。

    2.  リスト内のすべてのドライバーが処理するまでは、前の手順を繰り返します。 インクリメントするかどうかを確認、 *MemberIndex*パラメーターを[ **SetupDiEnumDriverInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdriverinfoa)その関数のリファレンス ページで説明されているとします。

    クラスのインストーラーは、ドライバーの一覧を変更、ERROR_DI_DO_DEFAULT を返します。 共同インストーラーは、ドライバーの一覧を変更する場合は、前処理で行う、NO_ERROR を返すにする必要があります。

-   デバイスの最適なドライバーを選択します。

    このアクションは、あまり一般的では、インストーラーは、デバイスの最適なドライバーを選択します。 このようなインストーラーが各ドライバーのデータを調べる、ドライバーを選択して呼び出すと[ **SetupDiSetSelectedDriver** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)ドライバーを設定します。 インストーラーでは、選択したドライバーを設定、NO_ERROR を返します。

    共同インストーラーを選択すると、ドライバー場合、処理後の実行にする必要があります。

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


[**SetupDiSelectBestCompatDrv**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiselectbestcompatdrv)

[**SetupDiSetSelectedDriver**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetselecteddrivera)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

 

 






