---
title: DIF_NEWDEVICEWIZARD_SELECT
description: DIF_NEWDEVICEWIZARD_SELECT
ms.assetid: b6b2eaf7-c87f-45d6-8845-6d03bde9a802
keywords:
- DIF_NEWDEVICEWIZARD_SELECT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_SELECT
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0192df62d3d4840b46116800ae07a47b00eb9d24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570224"
---
# <a name="difnewdevicewizardselect"></a>DIF_NEWDEVICEWIZARD_SELECT


DIF_NEWDEVICEWIZARD_SELECT 要求は、標準の [ドライバ] ページを置き換えるカスタム ウィザード ページを指定するインストーラーを許可します。 この要求は、非 PnP デバイスの手動インストール時にのみ使用されます。

### <a name="when-sent"></a>送信時

Windows では、「デバイス ドライバーを選択」ページが表示されます前にすぐに。

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
インストーラーを変更できる、 [ **SP_NEWDEVICEWIZARD_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff553305)カスタム ページを指定します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーがこの差分要求を処理しない場合は、前処理のパスから NO_ERROR を返します。 共同インストーラーがこの要求を処理する場合、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

ページが正常に渡された場合、クラスのインストーラーは NO_ERROR を返します。 それ以外の場合、クラスのインストーラーは、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

DIF_NEWDEVICEWIZARD_SELECT 要求は、標準の [ドライバ] ページを置き換えるカスタム ウィザード ページを指定するインストーラーを許可します。 この要求は、非 PnP デバイスの手動インストール時にのみ使用されます。

インストーラーは、標準の ドライバーのウィザード ページを完全に置き換えるには、この差分要求に応答します。 代わりに、インストーラーは、標準的なページを変更または選択できるドライバーの一覧を変更するだけに場合、インストーラーがで行うへの応答、 [ **DIF_SELECTDEVICE** ](dif-selectdevice.md)要求。

共同インストーラーは、クラスでは、処理後のパスと場合にのみ、カスタム ページを追加する必要がありますインストーラーは、カスタム ページを追加しませんでした。 クラスのインストーラーは、ページを追加する場合、共同インストーラーはいけない。 それ以外の場合、ユーザーの場合は、ドライバーを 2 回選択するよく寄せられる可能性があります。

インストーラーによって、カスタム ページの選択、インストーラーは、選択したドライバーを設定する必要があります。 ユーザーがクリックした後、ウィザード ページをサポートするインストーラーのコードで**次**、インストーラーを呼び出す必要があります[ **SetupDiSetSelectedDriver**](https://msdn.microsoft.com/library/windows/hardware/ff552183)します。

インストーラーには、Wizard 97 ヘッダーのタイトルとカスタム ウィザード ページの PROPSHEETPAGE 構造内のヘッダーのサブタイトルを指定する必要があります。 インストーラーは、ウィザードのシステム提供のタイトルを置き換えるいない必要があります。 PROPSHEETPAGE 構造体のドキュメントとプロパティのページの詳細については、Microsoft Windows SDK を参照してください。

差分のコードの詳細については、[DIF コードの処理](https://msdn.microsoft.com/library/windows/hardware/ff546094)を参照してください。

<a name="requirements"></a>必要条件
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

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](dif-newdevicewizard-postanalyze.md)

[**DIF_SELECTDEVICE**](dif-selectdevice.md)

[**SetupDiSetSelectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552176)

[**SetupDiSetSelectedDriver**](https://msdn.microsoft.com/library/windows/hardware/ff552183)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_NEWDEVICEWIZARD_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff553305)

 

 






