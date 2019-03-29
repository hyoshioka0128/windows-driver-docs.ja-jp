---
title: DEVPKEY_DeviceClass_LowerFilters
description: DEVPKEY_DeviceClass_LowerFilters
ms.assetid: 39bc784e-a8be-4921-9a12-f423fe502019
keywords:
- DEVPKEY_DeviceClass_LowerFilters デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_LowerFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5415eaf1f48d5788f8cdda76793dc51b5d7e2a0a
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464018"
---
# <a name="devpkeydeviceclasslowerfilters"></a>DEVPKEY_DeviceClass_LowerFilters


DEVPKEY_DeviceClass_LowerFilters デバイス プロパティは、のインストールされている下位レベルのフィルター ドライバーのサービス名の一覧を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_LowerFilters</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>データ形式</strong></p></td>
<td align="left"><p>"<em>service-name1</em>\0<em>service-name2</em>\0…<em>service-nameN</em>\0\0"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>インストール アプリケーションおよびインストーラー クラス フィルターをインストールした後で読み取り専用アクセス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_LOWERFILTERS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>LowerFilters</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

DEVPKEY_DeviceClass_LowerFilters の値は、クラス フィルター ドライバーのインストール時に設定されます。 クラスのフィルター ドライバーをインストールする方法の詳細については、次を参照してください。[フィルター ドライバーをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff547595)と[ **INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)します。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するにはLowerFilters します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_LowerFilters プロパティのキーをサポートしていません。 この以前のバージョンの Windows で、対応するアクセスすることでこのプロパティの値にアクセスできます**LowerFilters**クラスのレジストリ キーの下のレジストリ値。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、次を参照してください。[にアクセスするレジストリ エントリの値で、クラス レジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff537751)します。

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


[**INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

[**SetupDiOpenClassRegKeyEx**](https://msdn.microsoft.com/library/windows/hardware/ff552067)

 

 






