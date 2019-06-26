---
title: INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用してください。
description: INF AddProperty ディレクティブと INF DelProperty ディレクティブの使用
ms.assetid: e5ae8d66-b2dc-409e-bdac-9034a9e24672
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dac0f50c870a71d8236deda453177d895d72bf8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384750"
---
# <a name="using-the-inf-addproperty-directive-and-the-inf-delproperty-directive"></a>INF AddProperty ディレクティブと INF DelProperty ディレクティブの使用


Windows Vista および Windows の以降のバージョンで使用できます[ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md)と[ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md)に設定し、デバイスのインスタンスのプロパティを削除[デバイス セットアップ クラス](device-setup-classes.md)、[デバイス インターフェイス クラス](device-interface-classes.md)、およびデバイスのインターフェイス。 これが含まれています[デバイスのシステム定義プロパティ](system-defined-device-properties2.md)と[カスタム デバイス プロパティ](creating-custom-device-properties.md)します。 使用する場合に、次のガイドラインを使用する必要があります、 **AddProperty**と**DelProperty**ディレクティブの代わりに[ **INF AddReg ディレクティブ**](inf-addreg-directive.md)と[ **INF してディレクティブ**](inf-delreg-directive.md)を設定し、デバイスのプロパティを削除します。

-   Windows Vista および Windows の以降のバージョンで導入されたデバイスのプロパティを使用する必要があります**AddProperty**と**DelProperty**ディレクティブを設定し、デバイスのプロパティを削除します。

-   Windows Server 2003、Windows XP、または Windows 2000 で導入され、して設定できるデバイスのプロパティの**AddReg**ディレクティブおよびによって削除された、**して**ディレクティブを引き続き使用する必要があります**AddReg**と**して**ディレクティブを設定し、これらのデバイス プロパティを削除します。 使用しないようにする**AddProperty**と**DelProperty**ディレクティブ。

含めることができます、INF **AddProperty**ディレクティブと、INF **DelProperty**ディレクティブで、次の INF ファイルでセクションを設定し、デバイスのインスタンス、デバイス セットアップ クラス、デバイスのプロパティを削除インターフェイス クラス、およびデバイスのインターフェイス:

-   [**INF DDInstall セクション**](inf-ddinstall-section.md)

-   [**INF ClassInstall32 セクション**](inf-classinstall32-section.md)

-   *インストール-section インターフェイス*によって参照される、 [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)

-   *追加インターフェイス セクション*によって参照される、 [ **INF AddInterface ディレクティブ**](inf-addinterface-directive.md)

### <a name="using-the-inf-addproperty-directive"></a>INF AddProperty ディレクティブの使用

プロパティ値を変更するには、INF、 **AddProperty**ディレクティブ デバイス インスタンス、デバイス セットアップ クラスをデバイス インターフェイス クラス、またはデバイスのインターフェイスをインストールする」セクションでします。 **AddProperty**ディレクティブの参照が 1 つまたは複数*追加プロパティ セクション*プロパティを指定するエントリが含まれる、プロパティとプロパティを変更するために使用する値を変更する方法。 形式、 **AddProperty**ディレクティブを次に示します。

**AddProperty =** <em>追加プロパティ セクション</em>\[ **、** <em>追加プロパティ セクション</em>\] .

追加のプロパティ-セクション内の各行には、1 つのプロパティを指定します。 プロパティ情報を指定する 2 つの可能な行形式を次に示します。 表示される最初の行の形式では、その名前でプロパティを指定します。 この形式は、DEVPKEY_DrvPkg_ でのみ使用できます*Xxx*プロパティ。 2 番目の行の形式で、プロパティのカテゴリとプロパティ識別子に対応するプロパティを指定する[プロパティ キー](property-keys.md)します。 この 2 つ目の形式は、システム定義のプロパティを指定するために使用できる、または[カスタム デバイス プロパティ](creating-custom-device-properties.md)します。

**\[** <em>追加のプロパティ-セクション</em> **\]** 
<em>プロパティ名</em> **、、、\[** <em>フラグ</em> ** \]、** <em>値</em>
 **{** <em>プロパティ カテゴリの guid</em> **}、** <em>プロパティ pid</em> **、** <em>型</em> **、\[** <em>フラグ</em> ** \]、** <em>値</em>エントリの値は、次を指定します。

<a href="" id="property-name"></a>*property-name*  
DEVPKEY_DrvPkg_ を識別する名前*Xxx*プロパティ。 たとえば、 **DeviceModel**、表す、 [ **DEVPKEY_DrvPkg_Model** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-drvpkg-model)プロパティ、または**DeviceVendorWebSite**を表す、 [ **DEVPKEY_DrvPkg_VendorWebSite** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-drvpkg-vendorwebsite)プロパティ。

<a href="" id="property-category-guid"></a>*property-category-guid*  
プロパティが所属するプロパティのカテゴリの GUID 値。 など、システム定義[ **DEVPKEY_Device_FriendlyName** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-friendlyname)プロパティ。 GUID 値には、カスタム デバイス カテゴリも指定できます。

<a href="" id="property-pid"></a>*プロパティの pid*  
プロパティのカテゴリ内のプロパティを識別するプロパティの識別子。 たとえば、DEVPKEY_Device_FriendlyName プロパティの識別子のプロパティの値には 14 です。

<a href="" id="flags"></a>*フラグ*  
プロパティ値を変更する方法を示す省略可能なフラグ。

<a href="" id="type"></a>*型*  
A[プロパティ データ型識別子](property-data-type-identifiers.md)データ型を指定します。

<a href="" id="value"></a>*値*  
プロパティ値を変更するために使用する値。

次の例、 **AddProperty**ディレクティブに 2 つの行エントリが含まれています。 最初の行が含まれています、*プロパティ名*エントリの値"DeviceModel"および*値*エントリの値「サンプル デバイス モデル名」。 このエントリは、DEVPKEY_DrvPkg_Model プロパティを設定します。 2 番目の行エントリは、カスタム プロパティのカテゴリのカスタム プロパティを設定します。 *プロパティ カテゴリの guid*エントリの値は"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"および*プロパティ識別子*エントリの値は「2」 省略可能な*フラグ*エントリの値が存在しないと、*型*エントリの値が「18」(DEVPROP_TYPE_STRING)。 *値*エントリの値は「プロパティが 1 の文字列値」。

```cpp
[Root_Install.NT]
AddProperty=Root_AddProperty

[Root_AddProperty]
DeviceModel,,,,"Sample Device Model Name"
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 18,, "String value for property 1"
```

### <a name="using-the-inf-delproperty-directive"></a>INF DelProperty ディレクティブの使用

プロパティを削除するには、INF **DelProperty**ディレクティブ デバイス インスタンス、デバイス セットアップ クラスをデバイス インターフェイス クラス、またはデバイスのインターフェイスをインストールする」セクションでします。

主な目的、 [ **INF DelProperty ディレクティブ**](inf-delproperty-directive.md)は、デバイスのインストールを更新する INF ファイルで使用されます。 このような場合も、 **DelProperty**ディレクティブを使用して、以前のインストールによって設定された更新のインストールでは、不要になったプロパティを削除することができます。 使用して、 **DelProperty**ディレクティブ注意が必要です。 **DelProperty**システム コンポーネントによって、または別の INF ファイルによっても設定されているプロパティを削除するのには使えません。

**DelProperty**ディレクティブは、次の形式。

**DelProperty=** <em>del-property-section</em>\[ **,** <em>del-property-section</em>\] ...

内の各行を*del-section プロパティ*1 つのプロパティを指定します。 プロパティ情報を指定する 2 つの可能な行形式を次に示します。 表示される最初の行の形式では、その名前でプロパティを指定します。 この形式は、DEVPKEY_DrvPkg_ でのみ使用できます*Xxx*プロパティ。 2 番目の行の形式で、プロパティのカテゴリとプロパティ識別子に対応するプロパティを指定する[プロパティ キー](property-keys.md)します。 2 番目の形式は、システム定義のプロパティを指定するために使用できます、[カスタム デバイス プロパティ](creating-custom-device-properties.md)します。

**\[** <em>del-section プロパティ</em> **\]** 
*プロパティ名* \[ **、および***フラグ* \[ **、** <em>値</em>\] \] **{** <em>プロパティ カテゴリの guid</em> **}、** *プロパティ pid* \[ **、** *フラグ* \[ **、** <em>値</em>\] \]エントリの値は、次を指定します。

<a href="" id="property-name"></a>*property-name*  
DEVPKEY_DrvPkg_ を識別する名前*Xxx*プロパティ。 たとえば、 **DeviceModel**、表す、 [ **DEVPKEY_DrvPkg_Model** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-drvpkg-model)プロパティ、または**DeviceVendorWebSite**を表す、 [ **DEVPKEY_Device_FriendlyName** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-friendlyname)プロパティ。

<a href="" id="property-category-guid"></a>*property-category-guid*  
プロパティが所属するプロパティのカテゴリの GUID 値。 など、システム定義[ **DEVPKEY_Device_FriendlyName** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-friendlyname)プロパティ。 GUID 値には、カスタム デバイス カテゴリも指定できます。

<a href="" id="property-pid"></a>*プロパティの pid*  
プロパティのカテゴリ内のプロパティを識別するプロパティの識別子。 たとえば、DEVPKEY_Device_FriendlyName プロパティの識別子のプロパティの値には 14 です。

<a href="" id="flags"></a>*フラグ*  
データ型がプロパティでのみ使用するために有効なオプションのフラグ[ **DEVPROP_TYPE_STRING_LIST**](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string-list)します。 削除操作がで指定された文字列を削除フラグが設定されている場合*値*プロパティ文字列のリストから。

<a href="" id="value"></a>*値*  
プロパティ文字列の一覧から削除する文字列。

次の例を*del-section プロパティ*2 つの行エントリが含まれています。

最初の行が含まれています、*プロパティ名*エントリの値"DeviceModel"は、DEVPKEY_DrvPkg_Model プロパティを削除します。 2 番目の行エントリでは、データ型が DEVPROP_TYPE_STRING_LIST カスタム デバイス プロパティの値から文字列"DeleteThisString"を削除します。 2 番目の行で、*プロパティ カテゴリの guid*エントリの値は"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"、*プロパティ識別子*エントリの値は「2」、および*フラグ*エントリの値は"0x00000001"。

```cpp
[SampleDelPropertySection]
DeviceModel
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 0x00000001, "DeleteThisString"
```

 

 





