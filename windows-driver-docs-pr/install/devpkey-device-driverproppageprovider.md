---
title: DEVPKEY_Device_DriverPropPageProvider
description: DEVPKEY_Device_DriverPropPageProvider
ms.assetid: 9dabdba0-e179-467b-b0ad-960033a7ab86
keywords:
- DEVPKEY_Device_DriverPropPageProvider デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverPropPageProvider
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 51a2d8d6c8b91ec7b60d047dd43d4ba8b8879cb1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548779"
---
# <a name="devpkeydevicedriverproppageprovider"></a>DEVPKEY_Device_DriverPropPageProvider


DEVPKEY_Device_DriverPropPageProvider デバイス プロパティは、DLL、およびデバイスのインスタンスのプロパティ ページのプロバイダーとして登録されていると、DLL のエントリ ポイントの名前を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DriverPropPageProvider</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応するレジストリ値の識別子とレジストリ値の名前</strong></p></td>
<td align="left"><p>REGSTR_VAL_ENUMPROPPAGES_32</p>
<p><strong>EnumPropPages32</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

使用して DEVPKEY_Device_DriverPropPageProvider の値を設定することができます、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)に含まれている、 [ **INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)のデバイスをインストールする INF ファイル。

DEVPKEY_Device_DriverPropPageProvider の値を取得するには呼び出すことによって[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_DriverPropPageProvider プロパティのキーをサポートしていません。 この以前のバージョンの Windows で、対応するアクセスすることでこのプロパティの値にアクセスできます**EnumPropPages32**ソフトウェア キーをデバイス インスタンスの下のレジストリ値。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス ドライバーのプロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537732)します。

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
<td align="left"><p>Windows Vista および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






