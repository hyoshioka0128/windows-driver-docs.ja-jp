---
title: DEVPKEY_DeviceClass_UpperFilters
description: DEVPKEY_DeviceClass_UpperFilters
ms.assetid: 9a6a9587-340c-460e-b6e2-1aadfb5b8c2f
keywords:
- DEVPKEY_DeviceClass_UpperFilters デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_UpperFilters
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d411783efbcc7ac57fca58c21979085becbe4fb2
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463893"
---
# <a name="devpkeydeviceclassupperfilters"></a>DEVPKEY_DeviceClass_UpperFilters


DEVPKEY_DeviceClass_UpperFilters デバイス プロパティは、上位レベルのフィルター ドライバーのインストールされているは、サービス名の一覧を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_UpperFilters</p></td>
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
<td align="left"><p>SPCRP_UPPERFILTERS</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応するレジストリ値の名前</strong></p></td>
<td align="left"><p><strong>再</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

DEVPKEY_DeviceClass_UpperFilters の値は、クラス フィルター ドライバーのインストール時に設定されます。 クラスのフィルター ドライバーをインストールする方法の詳細については、[フィルター ドライバーをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff547595)と[ **INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)を参照してください。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するには再します。

Windows Server 2003、Windows XP、および Windows 2000 は、このプロパティをサポートは DEVPKEY_DeviceClass_UpperFilters プロパティのキーをサポートしていません。 この以前のバージョンの Windows で、対応するアクセスすることでこのプロパティの値にアクセスできます**再**クラスのレジストリ キーの下のレジストリ値。 Windows の以前のバージョンでこのプロパティの値にアクセスする方法については、[にアクセスするレジストリ エントリの値で、クラス レジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff537751)を参照してください。

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

 

 






