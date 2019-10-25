---
title: インストール後のデバイス オブジェクト レジストリ プロパティの設定
description: インストール後のデバイス オブジェクト レジストリ プロパティの設定
ms.assetid: e9415497-f61e-49ba-9376-9255e51e72a8
keywords:
- デバイスオブジェクト WDK カーネル、レジストリ
- レジストリ WDK デバイスオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 352be178c17be54a1db4faa2d95417fcdc3c9ad0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838429"
---
# <a name="setting-device-object-registry-properties-after-installation"></a>インストール後のデバイス オブジェクト レジストリ プロパティの設定





ユーザーモードプログラムでは、デバイスの[インストール機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))を使用して、ドライバーのデバイスオブジェクトのプロパティのレジストリ設定を取得または設定できます。 通常、これらの関数はインストールソフトウェアによって使用されますが、どのユーザーモードプログラムでも使用できます。 (プログラムは、管理者アクセス権を持つユーザーが実行する必要があります)。

[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)関数と[**SetupDiSetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceregistrypropertya)関数は、指定された各プロパティのレジストリキーを取得して設定します。 *Property*パラメーターは、取得または設定するプロパティを指定します。 *Propertybuffer*は、プロパティのコピー先のバッファー (プロパティを取得する場合) またはソースバッファー (プロパティを設定する場合) を指します。

*プロパティ*パラメーターの値と実際のプロパティの対応は次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th><em>Property</em>パラメーターの値</th>
<th>デバイスオブジェクトのプロパティ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SPDRP_CHARACTERISTICS</p></td>
<td><p>デバイスの特性</p></td>
</tr>
<tr class="even">
<td><p>SPDRP_DEVTYPE</p></td>
<td><p>Device type (デバイスの種類)</p></td>
</tr>
<tr class="odd">
<td><p>SPDRP_EXCLUSIVE</p></td>
<td><p>［排他］</p></td>
</tr>
<tr class="even">
<td><p>SPDRP_SECURITY</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_security_descriptor" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_security_descriptor)"><strong>SECURITY_DESCRIPTOR</strong></a>構造体としてのセキュリティ記述子</p></td>
</tr>
<tr class="odd">
<td><p>SPDRP_SECURITY_SDS</p></td>
<td><p>SDDL 文字列としてのセキュリティ記述子</p></td>
</tr>
</tbody>
</table>

 

セキュリティ記述子を取得または設定するには、2つの異なる方法が用意されていることに注意してください。 セキュリティ記述子を SDDL 文字列として扱うには、SPDRP\_セキュリティ値を指定してセキュリティ記述子をセキュリティ **\_記述子**構造体として扱うか、spdrp\_SECURITY\_SDS として扱うことができます。 SDDL 文字列の詳細については、「[デバイスオブジェクトの sddl](sddl-for-device-objects.md)」を参照してください。

Windows XP 以降のオペレーティングシステムでは、プログラムはデバイスセットアップクラスのプロパティ値を取得して設定することもできます。 Device setup クラスのプロパティ値を取得および設定するには、 [**Setupdigetclassregistryproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassregistrypropertya)関数と[**setupdigetclassregistryproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetclassregistrypropertya)関数を使用します。

**Setupdi * Xxx*** 関数の使用方法の詳細については、「[デバイスインストール機能の使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-device-installation-functions)」を参照してください。

 

 




