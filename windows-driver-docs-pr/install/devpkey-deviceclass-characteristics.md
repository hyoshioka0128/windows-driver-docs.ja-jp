---
title: DEVPKEY_DeviceClass_Characteristics
description: DEVPKEY_DeviceClass_Characteristics
ms.assetid: dd50a97b-7230-46a5-b6d2-0f741d7ae5d4
keywords:
- DEVPKEY_DeviceClass_Characteristics デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Characteristics
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 529164eb6008871299e140dbe4bbcd98c3a1159c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538644"
---
# <a name="devpkeydeviceclasscharacteristics"></a>DEVPKEY_DeviceClass_Characteristics


DEVPKEY_DeviceClass_Characteristics デバイス プロパティは、すべてのデバイスの既定のデバイスの特性を表す、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>プロパティのキー</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_Characteristics</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>データ型のプロパティの識別子</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プロパティへのアクセス</strong></p></td>
<td align="left"><p>インストール アプリケーションおよびデバイス セットアップ クラスをインストールした後、インストーラーによって、読み取り専用アクセス</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>対応する SPCRP_</strong><em>Xxx</em> <strong>識別子</strong></p></td>
<td align="left"><p>SPCRP_CHARACTERISTICS</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ローカライズか。</strong></p></td>
<td align="left"><p>X</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

インストール アプリケーションは、デバイス セットアップ クラスをインストールするときは、DEVPKEY_DeviceClass_Characteristics の値を設定できます。 デバイス セットアップ クラスと、このプロパティの設定をインストールする方法については、次を参照してください[ **INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)およびレジストリ エントリの値について **。DeviceCharacteristics**で提供されている、"特殊な*値のエントリ名*キーワード"のセクション[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)します。

DEVPKEY_DeviceClass_Characteristics の値は、FILE_DEVICE_ のビットごとの OR*Xxx*で定義されているフラグ*Wdm.h*と*Ntddk.h*します。 デバイスの特性の詳細については、次を参照してください。、 *DeviceCharacteristics*のパラメーター、 [ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)関数。

呼び出すことができます[ **SetupDiGetClassProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551086)または[ **SetupDiGetClassPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551090) DEVPKEY_DeviceClass_ の値を取得するには特性。

Windows Server 2003 および Windows XP は、このプロパティをサポートは DEVPKEY_DeviceClass_Characteristics プロパティのキーをサポートしていません。 この以前のバージョンの Windows では、このプロパティの値にアクセスするのに SPCRP_CHARACTERISTICS 識別子を使用できます。 このプロパティの値にアクセスする方法については、次を参照してください。[デバイス セットアップ クラス SPCRP_Xxx のプロパティを取得する](https://msdn.microsoft.com/library/windows/hardware/ff550644)します。

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


[**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)

[**INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)

[**INF ClassInstall32 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546335)

[**SetupDiGetClassProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551086)

[**SetupDiGetClassPropertyEx**](https://msdn.microsoft.com/library/windows/hardware/ff551090)

 

 






