---
title: DIF_POWERMESSAGEWAKE
description: DIF_POWERMESSAGEWAKE
ms.assetid: 73f6e763-0900-4297-ac88-20bbb3ac424d
keywords:
- DIF_POWERMESSAGEWAKE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_POWERMESSAGEWAKE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3b5876c1de677d30d351f86d6fd0befef99a6f71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532058"
---
# <a name="difpowermessagewake"></a>DIF_POWERMESSAGEWAKE


DIF_POWERMESSAGEWAKE 要求は、Windows がデバイスのプロパティの電源管理のプロパティ ページに表示されるカスタムのテキストを指定するインストーラーを使用します。

### <a name="when-sent"></a>送信時

ユーザーがデバイスのプロパティを表示するタブまたはメニュー項目をクリックしたとき。

Windows は、デバイスのドライバーは、電源管理をサポートしている場合にのみこの差分要求を送信します。 それ以外の場合、Windows では、デバイスの電源プロパティは表示されません。

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
[ **SP_POWERMESSAGEWAKE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553311)構造が関連付けられている、 *DeviceInfoData*します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
インストーラーを変更できる、 [ **SP_POWERMESSAGEWAKE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553311)デバイスの電源のプロパティ ページのカスタム テキストを指定します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーは、通常、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返します。

電源のプロパティのテキストが正常に渡された場合、クラスのインストーラーは NO_ERROR を返します。 それ以外の場合、クラスのインストーラーは、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

DIF_POWERMESSAGEWAKE 要求は、Windows がデバイスの電源のプロパティ ページに表示されるテキストを指定するインストーラーを使用します。

共同インストーラー power プロパティのテキストを提供する場合、処理後のフェーズで実行にする必要があります。 共同インストーラー共同インストーラーの前に要求を処理するインストーラーによって提供される power プロパティ テキストを上書きする場合は注意があります。

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


[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_POWERMESSAGEWAKE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553311)

 

 






