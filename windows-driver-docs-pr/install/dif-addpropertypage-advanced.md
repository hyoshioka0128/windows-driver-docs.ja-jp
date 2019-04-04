---
title: DIF_ADDPROPERTYPAGE_ADVANCED
description: DIF_ADDPROPERTYPAGE_ADVANCED
ms.assetid: d2b05c45-3536-4997-ac6f-a5b5c95a97da
keywords:
- DIF_ADDPROPERTYPAGE_ADVANCED デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_ADDPROPERTYPAGE_ADVANCED
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 661364e75d37b9f0515b155b1826a95949947cea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578757"
---
# <a name="difaddpropertypageadvanced"></a>DIF_ADDPROPERTYPAGE_ADVANCED


DIF_ADDPROPERTYPAGE_ADVANCED 要求には、デバイスの 1 つまたは複数のカスタム プロパティ ページを指定するインストーラーができます。

### <a name="when-sent"></a>送信時

デバイス マネージャーで、またはコントロール パネルの デバイスのプロパティで、ユーザーがクリックしたとき。

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
識別するハンドルを提供、[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)デバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
必要に応じてへのポインターを提供、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセット内のデバイスを識別する構造体。 場合*DeviceInfoSet*は**NULL**、Windows でのプロパティ ページを要求している、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイスのインストール パラメーター ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) に関連付けられている、 *DeviceInfoData*、指定した場合または、 *DeviceInfoSet*.

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_ADDPROPERTYPAGE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552337)構造が関連付けられている、 *DeviceInfoData*、指定した場合または、 *DeviceInfoSet*します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでは、デバイスのインストール パラメーターを変更できます。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
インストーラーを変更できる、 [ **SP_ADDPROPERTYPAGE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552337)カスタム ページを指定します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR または Win32 エラーを返すことができます。 共同インストーラーは、この差分要求 ERROR_DI_POSTPROCESSING_REQUIRED を返しませんする必要があります。

ページが正常に渡された場合、クラスのインストーラーは NO_ERROR を返します。 それ以外の場合、クラスのインストーラーは、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

この差分要求への応答では、インストーラーはカスタム プロパティ ページを提供できます。 この差分の要求を処理し、クラスのインストーラーまたは共同インストーラーからプロパティ ページを指定することができます、プロパティ ページのプロバイダーとして機能する別個の DLL の必要性を削除します。

通常、インストーラーは、新しいデバイスに固有またはセットアップ クラス固有のプロパティ ページを追加するには、この差分要求を処理します。 インストーラーでは、システムによって提供されるドライバーのプロパティ ページ、リソースのプロパティ ページ、またはデバイスのプロパティ ページを power を置き換えることもできます。 場合は、インストーラーに代わるシステム提供のページで、インストーラーする必要がありますフラグを設定、適切なデバイスのデバイスのインストール パラメーター。

<a href="" id="di-driverpage-added"></a>DI_DRIVERPAGE_ADDED  
インストーラーでは、ドライバのプロパティ ページを指定します。

<a href="" id="di-resourcepage-added"></a>DI_RESOURCEPAGE_ADDED  
インストーラーでは、リソースのプロパティ ページを指定します。

<a href="" id="di-flagsex-powerpage-added"></a>DI_FLAGSEX_POWERPAGE_ADDED  
インストーラーでは、電源のプロパティ ページを指定します。

インストーラーでは、システム提供の [全般] プロパティ ページを置き換えることはできません。

Windows には、[ドライバ] ページの 1 つ、1 つのリソース ページとデバイスの 1 つの電源ページのみが表示されます。 インストーラーは、前のインストーラーには、その型のページを既に提供されている場合の置き換えのシステム ページを指定しません。 この制約は、非システムが提供するプロパティ ページには適用されません。

共同インストーラーは、前処理のパスで、カスタム ページを追加する必要があります。

インストーラーでは、Windows を削除し、デバイスの再起動が必要なプロパティを設定するユーザーを許可している場合、インストーラーする必要がありますフラグを設定、DI_FLAGSEX_PROPCHANGE_PENDING デバイスからのインストール パラメーター、 **DialogProc**ルーチン.

デバイスのプロパティ ページを提供する方法の詳細については、[デバイスのプロパティ ページを提供する](https://msdn.microsoft.com/library/windows/hardware/ff549784)を参照してください。

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


[**SP_ADDPROPERTYPAGE_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552337)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

 

 






