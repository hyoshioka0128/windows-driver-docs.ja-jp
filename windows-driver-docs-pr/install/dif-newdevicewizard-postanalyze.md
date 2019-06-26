---
title: DIF_NEWDEVICEWIZARD_POSTANALYZE
description: DIF_NEWDEVICEWIZARD_POSTANALYZE
ms.assetid: 81d609e6-9562-4738-b3ba-c29b24612f91
keywords:
- DIF_NEWDEVICEWIZARD_POSTANALYZE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_POSTANALYZE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf4653ff7b50fb5d3b81562936d9444c0a74377a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387043"
---
# <a name="difnewdevicewizardpostanalyze"></a>DIF_NEWDEVICEWIZARD_POSTANALYZE


DIF_NEWDEVICEWIZARD_POSTANALYZE 要求により、デバイス ノードの後に、Windows がユーザーに表示されるウィザード ページを指定するインストーラー (*devnode*) が登録されている Windows デバイスのドライバーをインストールする前にします。 この要求は、非 PnP デバイスの手動インストール時にのみ使用されます。

### <a name="when-sent"></a>送信時

Windows は、前に、devnode「ライブ」ですが、デバイスを登録した後、Windows はデバイスのドライバーをインストールします。

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
[ **SP_NEWDEVICEWIZARD_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)構造が関連付けられている、 *DeviceInfoData*します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでは、デバイスのインストール パラメーターでフラグを変更できます。 Windows では、この差分要求の完了時にフラグをチェックしません。 ただし、インストール プロセスの後半でそれらをチェック、されます。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
インストーラーを変更できる、 [ **SP_NEWDEVICEWIZARD_DATA** ](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)カスタム ページを指定します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーがこの差分要求を処理しない場合は、前処理のパスから NO_ERROR を返します。 共同インストーラーがこの要求を処理する場合、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

ページが正常に渡された場合、クラスのインストーラーは NO_ERROR を返します。 それ以外の場合、クラスのインストーラーは、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

DIF_NEWDEVICEWIZARD_POSTANALYZE 要求は、devnode が登録されると、Windows デバイスのドライバーをインストールする前に、Windows がユーザーに表示されるウィザード ページを指定するインストーラーを使用します。 この要求は、非 PnP デバイスの手動インストール時にのみ使用されます。

カスタム インストーラーを追加した場合 postanalyze ページに、まず、インストーラーを確認する必要があるかどうか**NumDynamicPages**クラスのインストール パラメーターで MAX_INSTALLWIZARD_DYNAPAGES に達しました。

ユーザー後がクリックした**次**カスタム ページでは、Windows がデバイスのドライバーをインストールし、PnP マネージャーがデバイスを開始します。 Postanalyze ウィザード ページは、ドライバーが読み込まれ、デバイスが起動する前に作業を実行するインストーラーの最後の機会です。

インストーラーには、Wizard 97 ヘッダーのタイトルとカスタム ウィザード ページの PROPSHEETPAGE 構造内のヘッダーのサブタイトルを指定する必要があります。 インストーラーは、ウィザードのシステム提供のタイトルを置き換えるいない必要があります。 PROPSHEETPAGE 構造体のドキュメントとプロパティのページの詳細については、Microsoft Windows SDK を参照してください。

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


[**DIF_NEWDEVICEWIZARD_PREANALYZE**](dif-newdevicewizard-preanalyze.md)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](dif-newdevicewizard-preselect.md)

[**DIF_NEWDEVICEWIZARD_SELECT**](dif-newdevicewizard-select.md)

[**SP_DEVINFO_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinfo_data)

[**SP_DEVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_devinstall_params_a)

[**SP_NEWDEVICEWIZARD_DATA**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_newdevicewizard_data)

 

 






