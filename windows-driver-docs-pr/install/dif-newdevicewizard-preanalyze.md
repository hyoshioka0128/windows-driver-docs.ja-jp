---
title: DIF_NEWDEVICEWIZARD_PREANALYZE
description: DIF_NEWDEVICEWIZARD_PREANALYZE
ms.assetid: 6731a916-488a-4fb2-84d9-4b3cb9b8b160
keywords:
- DIF_NEWDEVICEWIZARD_PREANALYZE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_PREANALYZE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2843a4b06882f6bda894c9102bcf0838477e48ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380742"
---
# <a name="difnewdevicewizardpreanalyze"></a>DIF_NEWDEVICEWIZARD_PREANALYZE


DIF_NEWDEVICEWIZARD_PREANALYZE 要求は、分析ページを表示する前に、Windows がユーザーに表示されるウィザード ページを指定するインストーラーを許可します。 この要求は、非 PnP デバイスの手動インストール時にのみ使用されます。

### <a name="when-sent"></a>送信時

デバイス ノードにより、Windows デバイスを登録する前に、ユーザーが、ドライバーを選択した後 (*devnode*)「ライブ」です。

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
識別するハンドルを提供、[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)デバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_NEWDEVICEWIZARD_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff553305)構造が関連付けられている、 *DeviceInfoData*します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでは、デバイスのインストール パラメーターでフラグを変更できます。 Windows では、この差分要求の完了時にフラグをチェックしません。 ただしに後で、インストール プロセスにチェックインします。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
インストーラーを変更できる、 [ **SP_NEWDEVICEWIZARD_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff553305)カスタム ウィザード ページを指定します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーがこの差分要求を処理しない場合は、前処理のパスから NO_ERROR を返します。 共同インストーラーがこの要求を処理する場合、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

ページが正常に渡された場合、クラスのインストーラーは NO_ERROR を返します。 それ以外の場合、クラスのインストーラーは、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

DIF_NEWDEVICEWIZARD_PREANALYZE 要求は、分析ページを表示する前に、Windows がユーザーに表示されるウィザード ページを指定するインストーラーを許可します。 これらのページは、"postselect"ページとして考えることができます。 この要求は、非 PnP デバイスの手動インストール時にのみ使用されます。

インストーラーでは、モデム デバイスを選択した後は、COM ポートを選択する、カスタム preanalyze ページをたとえば、使用可能性があります。

カスタム インストーラーを追加した場合事前選択ページに、まず、インストーラーを確認する必要があるかどうか**NumDynamicPages**クラスのインストール パラメーターで MAX_INSTALLWIZARD_DYNAPAGES に達しました。

インストーラーには、Wizard 97 ヘッダーのタイトルとカスタム ウィザード ページの PROPSHEETPAGE 構造内のヘッダーのサブタイトルを指定する必要があります。 インストーラーは、ウィザードのシステム提供のタイトルを置き換えるいない必要があります。 PROPSHEETPAGE 構造体のドキュメントとプロパティのページの詳細については、Microsoft Windows SDK を参照してください。

差分のコードの詳細については、次を参照してください。 [DIF コードの処理](https://msdn.microsoft.com/library/windows/hardware/ff546094)します。

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


[**DIF_NEWDEVICEWIZARD_PRESELECT**](dif-newdevicewizard-preselect.md)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](dif-newdevicewizard-postanalyze.md)

[**DIF_NEWDEVICEWIZARD_SELECT**](dif-newdevicewizard-select.md)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_NEWDEVICEWIZARD_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff553305)

 

 






