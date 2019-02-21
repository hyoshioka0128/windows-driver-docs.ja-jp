---
title: DEVPKEY_Device_MatchingDeviceId
description: DEVPKEY_Device_MatchingDeviceId
ms.assetid: 4695c713-0586-42be-9dd7-7da5bd87a3c0
keywords:
- DEVPKEY_Device_MatchingDeviceId デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_MatchingDeviceId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8348b275652f6bc03f35c85acdcaaa686db52b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536187"
---
# <a name="devpkeydevicematchingdeviceid"></a>DEVPKEY_Device_MatchingDeviceId


DEVPKEY_Device_MatchingDeviceId デバイス プロパティを表します、[ハードウェア ID](https://msdn.microsoft.com/library/windows/hardware/ff546152)または[互換性 ID](https://msdn.microsoft.com/library/windows/hardware/ff539950) Windows を使用してデバイス インスタンスをインストールします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_MatchingDeviceId</p></td>
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
<td align="left"><p>REGSTR_VAL_MATCHINGDEVICEID</p>
<p><strong>MatchingDeviceId</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Windows では、DEVPKEY_Device_MatchingDeviceId の値を設定します。 ハードウェア Id とデバイスの互換性 Id がによって提供される、*デバイス説明*エントリに含まれている、 [ **INF*モデル*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)のデバイスをインストールする INF ファイル。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) PKEY_Device_MatchingDeviceId の値を取得します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_Device_MatchingDeviceId プロパティのキーをサポートしていません。 この以前のバージョンの Windows で、対応するアクセスすることでこのプロパティの値にアクセスできます**MatchingDeviceId**ソフトウェア キーをデバイス インスタンスの下のレジストリ値。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[デバイス ドライバーのプロパティへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff537732)します。

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


[**INF*モデル*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

 

 






