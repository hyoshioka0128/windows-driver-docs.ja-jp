---
title: DEVPKEY_Device_SafeRemovalRequired
description: DEVPKEY_Device_SafeRemovalRequired
ms.assetid: a162e259-21aa-40d9-a65a-af175a59df6a
keywords:
- DEVPKEY_Device_SafeRemovalRequired デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SafeRemovalRequired
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fd7ffd441ad6460f0ea5992da68c21b6d40696ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581992"
---
# <a name="devpkeydevicesaferemovalrequired"></a>DEVPKEY_Device_SafeRemovalRequired


DEVPKEY_Device_SafeRemovalRequired デバイス プロパティは、ホット プラグ デバイス インスタンスがコンピューターからの安全な取り外しを必要とするかどうかを示すブール値を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_Device_SafeRemovalRequired</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>アプリケーションをインストールし、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>いいえ</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

ホット プラグ デバイス インスタンスに対してこのプロパティは、DEVPROP_TRUE の値を持つ、デバイス インスタンスには、コンピューターからの安全な取り外しが必要です。 この場合は、Windows の表示、**ハードウェアの安全な**タスク バーの右側にある通知領域にアイコン。 ユーザーは、このアイコンをクリックすると、システムの起動時、**ハードウェアの安全な**プログラム。 このプログラムを使用すると、ユーザーはコンピューターから突然削除できる前に、削除のデバイスのインスタンスを準備するシステムに指示できます。

**注**  デバイス インスタンスが挿入されるメディアが必要し、DEVPROP_TRUE の DEVPKEY_Device_SafeRemovalRequired プロパティ値を持つ必要がありますデバイス インスタンスが、光学ディスク ドライブなどのリムーバブル メディア デバイスの場合。 デバイスのインスタンスが表示される両方に該当する場合、**ハードウェアの安全な**プログラム。

 

Windows のプラグ アンド プレイ (PnP) は、ホット プラグ デバイス インスタンスでは、次の場合、システムから安全な取り外しが必要であるを決定します。

-   デバイス インスタンスは、システムに現在接続されています。

-   デバイス インスタンスが開始されたか、または、システムによって自動的に取り出すことができます。

-   デバイス インスタンス CM_DEVCAP_SURPRISEREMOVALOK デバイス機能のビットが設定されていません。 デバイスの機能の詳細については、次を参照してください。 [ **SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)します。

-   デバイス インスタンスが持っていない、 [ **DEVPKEY_Device_SafeRemovalRequiredOverride** ](devpkey-device-saferemovalrequiredoverride.md)デバイス プロパティ DEVPROP_FALSE に設定します。

    **注**  無条件 pnp DEVPROP_TRUE に DEVPKEY_Device_SafeRemovalRequiredOverride デバイスのプロパティが設定されている場合、ホット プラグ デバイスが安全な取り外し必要であります。

     

-   デバイス インスタンスがあるか、その親デバイス インスタンスから直接リムーバブル リムーバブル先祖、そのデバイス ツリーまたはします。

呼び出すことができます[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963) DEVPKEY_Device_SafeRemovalRequired の値を取得します。

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
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h (Devpkey.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVPKEY_Device_SafeRemovalRequiredOverride**](devpkey-device-saferemovalrequiredoverride.md)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)

 

 






