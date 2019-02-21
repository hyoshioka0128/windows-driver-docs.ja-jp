---
title: DEVPKEY_DeviceClass_Security
description: DEVPKEY_DeviceClass_Security
ms.assetid: e23fd11b-07ee-4375-841d-1fa9c42d5a28
keywords:
- DEVPKEY_DeviceClass_Security デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Security
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bba431e210bb4924f2699e3c72d6b4a72fd54294
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553148"
---
# <a name="devpkeydeviceclasssecurity"></a>DEVPKEY_DeviceClass_Security


DEVPKEY_DeviceClass_Security デバイス プロパティは、のセキュリティ記述子構造体を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_Security</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-security-descriptor.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR&lt;/strong&gt;](devprop-type-security-descriptor.md)"><strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアクセス アプリケーションをインストールしてインストーラー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_SECURITY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

値を設定する DEVPKEY_DeviceClass_Security 中またはインストール後のアプリケーションは、デバイス セットアップ クラスをインストールします。 このプロパティを設定する方法の詳細については、次を参照してください。[セキュリティで保護されたデバイスのインストールを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540212)します。

DEVPKEY_DeviceClass_Security の値を取得するには呼び出すことによって[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090). 呼び出して DEVPKEY_DeviceClass_Security を設定する[ **SetupDiSetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552128)または[ **SetupDiSetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff552132)します。

Windows Server 2003 および Windows XP は、このプロパティをサポートは DEVPKEY_DeviceClass_Security プロパティのキーをサポートしていません。 この以前のバージョンの Windows では、このプロパティの値にアクセスするのに SPCRP_SECURITY 識別子を使用できます。 このプロパティの値にアクセスする方法については、次を参照してください。[デバイス セットアップ クラス SPCRP_Xxx のプロパティを取得する](https://msdn.microsoft.com/library/windows/hardware/ff550644)と[デバイス セットアップ クラス SPCRP_Xxx プロパティの設定](https://msdn.microsoft.com/library/windows/hardware/ff550814)します。

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


[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiSetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552128)

[**SetupDiSetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff552132)

 

 






