---
title: DEVPKEY_DeviceClass_SecuritySDS
description: DEVPKEY_DeviceClass_SecuritySDS
ms.assetid: 463e8af1-a1cc-4c05-94c9-f1fbaf5928f9
keywords:
- DEVPKEY_DeviceClass_SecuritySDS デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_SecuritySDS
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 66306349c0bd048fd6db8d8d1f10eb1bdbe2d586
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551561"
---
# <a name="devpkeydeviceclasssecuritysds"></a>DEVPKEY_DeviceClass_SecuritySDS


DEVPKEY_DeviceClass_SecuritySDS デバイス プロパティは、のセキュリティ記述子文字列を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_SecuritySDS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-security-descriptor-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING&lt;/strong&gt;](devprop-type-security-descriptor-string.md)"><strong>DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアクセス アプリケーションをインストールしてインストーラー</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_SECURITY_SDS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

値を設定する DEVPKEY_DeviceClass_SecuritySDS 中またはインストール後のアプリケーションは、デバイス セットアップ クラスをインストールします。 このプロパティを設定する方法の詳細については、[セキュリティで保護されたデバイスのインストールを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540212)を参照してください。

DEVPKEY_DeviceClass_SecuritySDS の値を取得するには呼び出すことによって[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090). 呼び出して DEVPKEY_DeviceClass_SecuritySDS を設定する[ **SetupDiSetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552128)または[ **SetupDiSetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff552132)します。

Windows Server 2003 および Windows XP は、このプロパティをサポートは DEVPKEY_DeviceClass_SecuritySDS プロパティのキーをサポートしていません。 この以前のバージョンの Windows では、このプロパティの値にアクセスするのに SPCRP_SECURITY_SDS 識別子を使用できます。 このプロパティの値にアクセスする方法については、[デバイス セットアップ クラス SPCRP_Xxx のプロパティを取得する](https://msdn.microsoft.com/library/windows/hardware/ff550644)と[デバイス セットアップ クラス SPCRP_Xxx プロパティの設定](https://msdn.microsoft.com/library/windows/hardware/ff550814)を参照してください。

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

 

 






