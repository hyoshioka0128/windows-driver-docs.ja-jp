---
title: DIF_UNREMOVE
description: DIF_UNREMOVE
ms.assetid: 01e39f77-3ee8-44c4-ba1a-19d4356b26ce
keywords:
- DIF_UNREMOVE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_UNREMOVE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 50ba389144299d7af774b74d186490d065010896
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538646"
---
# <a name="difunremove"></a>DIF_UNREMOVE


Windows が特定のハードウェア プロファイル内のデバイスを復元しようと、インストーラー、操作に参加する機会が与えられます、DIF_UNREMOVE 要求は、インストーラーを通知します。 Windows では、非 PnP デバイスは、この要求のみ送信します。

### <a name="when-sent"></a>送信時

ときに、ハードウェア プロファイルをルートで列挙される、非 PnP デバイスが再開されます。

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
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_UNREMOVEDEVICE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553349)構造が関連付けられている、 *DeviceInfoData*します。 **スコープ**DI_UNREMOVEDEVICE_CONFIGSPECIFIC にフィールドを設定する必要があり、ハードウェア プロファイルを指定する必要があります、 **HwProfile**フィールド。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="none"></a>[なし]  

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、[既定 DIF コード ハンドラーを呼び出す](https://msdn.microsoft.com/library/windows/hardware/ff537868)を参照してください。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiUnremoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552193)

### <a name="installer-operation"></a>インストーラーの操作

"Unremoving"デバイスを基本的には、Windows が特定のハードウェア プロファイルで「存在しない」としてデバイスを対象としてマーク済みフラグをクリアすることを意味します。

差分のコードの詳細については、[DIF コードの処理](https://msdn.microsoft.com/library/windows/hardware/ff546094)を参照してください。

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


[**SetupDiUnremoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552193)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_UNREMOVEDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553349)

 

 






