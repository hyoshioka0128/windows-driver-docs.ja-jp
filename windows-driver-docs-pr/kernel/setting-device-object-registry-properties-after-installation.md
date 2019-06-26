---
title: インストール後のデバイス オブジェクト レジストリ プロパティの設定
description: インストール後のデバイス オブジェクト レジストリ プロパティの設定
ms.assetid: e9415497-f61e-49ba-9376-9255e51e72a8
keywords:
- デバイス オブジェクトの WDK カーネル、レジストリ
- レジストリの WDK デバイス オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b5b81f71b3e2a2827aad3581cb6e596a11bd5d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360279"
---
# <a name="setting-device-object-registry-properties-after-installation"></a>インストール後のデバイス オブジェクト レジストリ プロパティの設定





ユーザー モードのプログラムで使用できる、[デバイスのインストール機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))を取得またはドライバーのデバイス オブジェクトのプロパティのレジストリ設定を設定します。 インストール ソフトウェアをこれらの関数を使用する通常が、それらを任意のユーザー モードのプログラムで使用することができます。 (プログラムは管理者アクセス権を持つユーザーで実行する必要があります)。

[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)と[ **SetupDiSetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)関数を取得およびレジストリ キーの設定各プロパティを指定します。 *プロパティ*パラメーターを取得または設定するプロパティを指定します。 *PropertyBuffer*プロパティ (プロパティの設定) 場合にコピー先のバッファー (する場合、プロパティの取得) またはソースへのポインターがバッファーします。

値の間の通信、*プロパティ*パラメーターと実際のプロパティを次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>場合は値<em>プロパティ</em>パラメーター</th>
<th>デバイス オブジェクトのプロパティ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SPDRP_CHARACTERISTICS</p></td>
<td><p>デバイスの特性</p></td>
</tr>
<tr class="even">
<td><p>SPDRP_DEVTYPE</p></td>
<td><p>デバイスの種類</p></td>
</tr>
<tr class="odd">
<td><p>SPDRP_EXCLUSIVE</p></td>
<td><p>［排他］</p></td>
</tr>
<tr class="even">
<td><p>SPDRP_SECURITY</p></td>
<td><p>セキュリティ記述子として、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_security_descriptor" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_security_descriptor)"> <strong>SECURITY_DESCRIPTOR</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td><p>SPDRP_SECURITY_SDS</p></td>
<td><p>SDDL 文字列としてのセキュリティ記述子</p></td>
</tr>
</tbody>
</table>

 

取得またはセキュリティ記述子を設定する 2 つの方法は提供されることに注意してください。 SPDRP を指定する\_セキュリティの値として、セキュリティ記述子を扱う、**セキュリティ\_記述子**構造体、または SPDRP\_セキュリティ\_SDS、セキュリティを処理するにはSDDL 文字列としての記述子。 SDDL 文字列の詳細については、次を参照してください。[デバイス オブジェクトの SDDL](sddl-for-device-objects.md)します。

Windows XP と以降のオペレーティング システムでは、プログラムも取得し、デバイス セットアップ クラスのプロパティ値を設定できます。 使用して、 [ **SetupDiGetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)と[ **SetupDiSetClassRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)関数、プロパティを取得および設定デバイス セットアップ クラスの値。

使用しての詳細については、 **SetupDi * Xxx*** 関数を参照してください[デバイス インストールの機能を使用して](https://docs.microsoft.com/windows-hardware/drivers/install/using-device-installation-functions)します。

 

 




