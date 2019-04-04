---
title: DEVPKEY_DeviceClass_ClassCoInstallers
description: DEVPKEY_DeviceClass_ClassCoInstallers
ms.assetid: c1369006-5329-48c7-afe0-ddce44889bbc
keywords:
- DEVPKEY_DeviceClass_ClassCoInstallers デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_ClassCoInstallers
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25ae30272396b1a31b699e730dfcb0e3017adc85
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464104"
---
# <a name="devpkeydeviceclassclasscoinstallers"></a>DEVPKEY_DeviceClass_ClassCoInstallers


DEVPKEY_DeviceClass_ClassCoInstallers デバイス プロパティがインストールされているクラスの共同インストーラーの一覧を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_ClassCoInstallers</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データ形式</strong></p></td>
<td align="left"><p>"<em>coinstaller1.dll</em>、<em>coinstaller1 エントリ ポイント</em>\0.<em>coinstallerN.dll</em>、<em>coinstallerN エントリ ポイント</em>\0\0"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>読み取りおよび書き込みアクセス アプリケーションをインストールしてインストーラー</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>HLM\System\CurrentControlSet\Control\CoDeviceInstallers{</strong><em>device-setup-class-guid</em><strong>}</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

クラスの共同インストーラー リスト内の各クラス インストーラーは、その DLL とエントリ ポイントで識別されます。

クラスの共同インストーラーをインストールする方法については、[クラス共同インストーラーを登録する](https://msdn.microsoft.com/library/windows/hardware/ff549801)を参照してください。

DEVPKEY_DeviceClass_ClassCoInstallers の値を取得するには呼び出すことによって[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090). 呼び出して DEVPKEY_DeviceClass_ClassCoInstallers を設定する[ **SetupDiSetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552128)または[ **SetupDiSetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552132).

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_ClassCoInstallers プロパティのキーをサポートしていません。 Windows の以前のバージョンに対応する情報にアクセスする方法については、[デバイス セットアップ クラスの共同インストーラー レジストリ エントリの値にアクセスする](https://msdn.microsoft.com/library/windows/hardware/ff537754)を参照してください。

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

 

 






