---
title: INF AddProperty ディレクティブ
description: AddProperty ディレクティブは、デバイスインスタンス、デバイスセットアップクラス、デバイスインターフェイスクラス、またはデバイスインターフェイスに設定されているデバイスプロパティを変更する1つ以上の INF ファイルセクションを参照します。
ms.assetid: 8fcb1355-f13d-4d96-aa73-62a094a52267
keywords:
- INF AddProperty ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddProperty Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b91ae3fbc4c7b2164499e5a121658523a0c47f0
ms.sourcegitcommit: ea42499bb6c405abaa8b1093afa741cd3910da66
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619776"
---
# <a name="inf-addproperty-directive"></a>INF AddProperty ディレクティブ


**Addproperty**ディレクティブは、デバイスインスタンス、[デバイスセットアップクラス](device-setup-classes.md)、[デバイスインターフェイスクラス](device-interface-classes.md)、またはデバイスインターフェイスに設定されている[デバイスプロパティ](device-properties.md)を変更する1つ以上の INF ファイルセクションを参照します。

```inf
[DDInstall] |
[DDInstall.nt] |
[DDInstall.ntx86] |
[DDInstall.ntia64] |
[DDInstall.ntamd64] |
[DDInstall.ntarm] |
[DDInstall.ntarm64]
[ClassInstall32] | 
[ClassInstall32.nt] | 
[ClassInstall32.ntx86] |
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  |  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  |  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  |  (Windows 10 and later versions of Windows)
[interface-install-section] | 
[interface-install-section.nt] | 
[interface-install-section.ntx86] | 
[interface-install-section.ntia64] |  (Windows XP and later versions of Windows)
[interface-install-section.ntamd64]  (Windows XP and later versions of Windows) |
[interface-install-section.ntarm]  (Windows 8 and later versions of Windows) |
[interface-install-section.ntarm64]  (Windows 10 and later versions of Windows)
[add-interface-section]

AddProperty=add-property-section[,add-property-section]...  (Windows Vista and later versions of Windows)
...
```

各*プロパティセクション*には、次の操作を行うためのエントリを含めることができます。

-   デバイスプロパティを追加し、プロパティの値を初期化します。
-   既存のデバイスプロパティの値を変更します。

**Addproperty**ディレクティブによって参照される*追加のプロパティセクション*には、次の形式があります。

```inf
[add-property-section]
(property-name, , , [flags], value]) | 
({property-category-guid}, property-pid, type, [flags], value)
...
```

[プロパティの追加] セクションには、任意の数の*プロパティ名*エントリまたは*プロパティ guid*エントリを含めることができます。それぞれの行は別個の行にあります。

## <a name="entries"></a>エントリ


<a href="" id="property-name"></a>*プロパティ名*  
デバイスインスタンス[ドライバーパッケージ](driver-packages.md)のプロパティを表す、次のプロパティ名のいずれかです。

-   **DeviceModel**
-   **DeviceVendorWebsite**
-   **DeviceDetailedDescription**
-   **Devicedocumentation のリンク**
-   **DeviceIcon**
-   **DeviceBrandingIcon**

カスタムデバイスアイコンの追加の詳細については、「[デバイスのアイコンの提供](providing-vendor-icons-for-the-shell-and-autoplay.md)」を参照してください。

<a href="" id="property-category-guid"></a>*プロパティ-カテゴリ-guid*  
プロパティカテゴリを識別する GUID 値。 GUID 値には、デバイスインスタンス、デバイス[セットアップクラス](device-setup-classes.md)、[デバイスインターフェイスクラス](device-interface-classes.md)、またはデバイスインターフェイスのプロパティカテゴリの1つを識別するシステム定義の guid を指定できます。 同じ GUID 値を持つすべてのプロパティは、同じカテゴリのメンバーです。 これらのプロパティカテゴリは、 *Devpkey*で定義されています。

GUID 値には、カスタムプロパティカテゴリを識別するカスタム GUID 値を指定することもできます。

<a href="" id="property-pid"></a>*プロパティ-pid*  
プロパティカテゴリ内の特定のプロパティを示すプロパティ識別子。このプロパティは、*カテゴリ guid*値によって示されます。 内部システムの理由により、プロパティ識別子は2以上である必要があります。

<a href="" id="type"></a>各種  
プロパティ- *category-guid*値および*プロパティ-pid*値で指定されたプロパティの[データ型識別子](https://docs.microsoft.com/previous-versions/ff541476(v=vs.85))の、10進数形式または16進数形式の数値。 次の[**基本データ型**](https://docs.microsoft.com/previous-versions/ff537793(v=vs.85))のみがサポートされています。

-   DEVPROP_TYPE_STRING
-   DEVPROP_TYPE_STRING_LIST
-   DEVPROP_TYPE_BINARY
-   DEVPROP_TYPE_BOOLEAN
-   DEVPROP_TYPE_UINT32

たとえば、DEVPROP_TYPE_STRING データ型の10進値は 18 (0x00000012) で、DEVPROP_TYPE_STRING_LIST データ型の10進値は 2066 (0x00002012) です。

<a href="" id="flags"></a>*示す*  
追加操作を制御する次のフラグのビットごとの OR である、省略可能な16進値。

<a href="" id="0x00000001--flg-addproperty-noclobber--"></a>**0x00000001** (FLG_ADDPROPERTY_NOCLOBBER)   
値のエントリ値によって既存のプロパティ値が置換されないようにするフラグ。 **インクルード**および**必要**なディレクティブを使用してプロパティをオーバーライドできるようにする場合、ライターはそのプロパティに対してこのフラグを指定する必要があります。 これは、 **windows が**インクルードおよび**必要**なディレクティブを含む inf セクション内の他のすべてのディレクティブを処理した後に、 **include** **ディレクティブに**よって参照されている inf セクションを windows が処理するためです。

<a href="" id="0x00000002--flg-addproperty-overwriteonly--"></a>**0x00000002** (FLG_ADDPROPERTY_OVERWRITEONLY)   
指定したプロパティが既に存在する場合にのみ、プロパティ値を値のエントリ値に設定するフラグ。

<a href="" id="0x00000004--flg-addproperty-append--"></a>**0x00000004** (FLG_ADDPROPERTY_APPEND)   
既存のプロパティ文字列値の値エントリ値を追加するフラグ。 このフラグは、プロパティのデータ型が DEVPROP_TYPE_STRING_LIST 場合にのみ有効です。 指定された文字列が既存の文字列値に既に存在する場合、指定された文字列は既存のプロパティ文字列値に追加されません。

<a href="" id="0x00000008--flg-addproperty-or-"></a>**0x00000008** (FLG_ADDPROPERTY_OR)  
値エントリ値のビットごとの OR を、既存のプロパティ値との間で実行するフラグ。 このフラグは、プロパティのデータ型が DEVPROP_TYPE_UINT32 場合にのみ有効です。

<a href="" id="0x00000010--flg-addproperty-and-"></a>**0x00000010** (FLG_ADDPROPERTY_AND)  
値エントリ値のビットごとの AND を、既存のプロパティ値との間で実行するフラグ。 このフラグは、プロパティのデータ型が DEVPROP_TYPE_UINT32 場合にのみ有効です。

<a href="" id="value"></a>*value*  
プロパティのデータ型および*flags*エントリの値に応じて、プロパティ値を変更するために追加操作が使用する値。

<a name="remarks"></a>解説
-------

**Addproperty**ディレクティブは、システム定義のデバイスプロパティまたはカスタムデバイスプロパティを変更するために使用できます。 このディレクティブは、上記の仮構文ステートメントに示されているいずれかのセクションの下で指定できます。

各*追加プロパティセクション*の名前は、inf ファイル内で一意である必要がありますが、同じ inf ファイル内の複数の**addproperty**ディレクティブでセクションを参照することはできます。 各セクション名は、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」で説明されているセクション名を定義するための一般的な規則に従う必要があります。

INF **Addproperty**ディレクティブの使用方法の詳細については、「 [Inf addproperty ディレクティブと Inf Delproperty ディレクティブの使用](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)」を参照してください。

<a name="examples"></a>例
--------

Add property セクションの次の例には、2つの行エントリが含まれています。最初の行のエントリは、 **DeviceModel**プロパティを名前で設定し、2行目のエントリはカスタムプロパティキー GUID を指定することによってカスタムデバイスプロパティを設定します。

最初の行には、*プロパティ名*のエントリ値 "DeviceModel" と*値*のエントリ値 "サンプルデバイスモデル名" が含まれています。

2行目のエントリは、カスタムプロパティカテゴリのカスタムプロパティを設定します。 プロパティ-category-guid エントリの値は "c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e" で、プロパティ識別子のエントリ値は "2" です。

省略可能な*フラグ*エントリの値が存在せず、型エントリの値が "18" (DEVPROP_TYPE_STRING) です。 値のエントリ値は、"プロパティ1の文字列値" です。

```inf
[SampleAddPropertySection]
DeviceModel,,,,"Sample Device Model Name"
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 18,, "String value for property 1"
```

## <a name="see-also"></a>関連項目


[**DelProperty**](inf-delproperty-directive.md)

 

 






