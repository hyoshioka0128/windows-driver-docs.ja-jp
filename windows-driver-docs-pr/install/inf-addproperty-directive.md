---
title: INF AddProperty ディレクティブ
description: AddProperty ディレクティブは、デバイス インスタンス、デバイス セットアップ クラスをデバイス インターフェイス クラス、またはデバイスのインターフェイスに設定されているデバイスのプロパティを変更する 1 つまたは複数の INF ファイルでセクションを参照します。
ms.assetid: 8fcb1355-f13d-4d96-aa73-62a094a52267
keywords:
- INF AddProperty ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF AddProperty Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3af574a8deeac086922eca11a811b8e717d1ca7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390749"
---
# <a name="inf-addproperty-directive"></a>INF AddProperty ディレクティブ


**AddProperty**ディレクティブを変更する 1 つまたは複数の INF ファイルでセクションを参照して、[デバイス プロパティ](device-properties.md)デバイス インスタンスの場合に設定されている、[デバイス セットアップ クラス](device-setup-classes.md)、 [デバイス インターフェイス クラス](device-interface-classes.md)、またはデバイスのインターフェイス。

```ini
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

各*追加プロパティ セクション*以下を実行するエントリがあることができます。

-   デバイスのプロパティを追加し、プロパティの値を初期化します。
-   既存のデバイス プロパティの値を変更します。

*追加プロパティ セクション*によって参照される、 **AddProperty**ディレクティブは、次の形式。

```ini
[add-property-section]
(property-name, , , [flags], value]) | 
({property-category-guid}, property-pid, type, [flags], value)
...
```

追加のプロパティ セクションでは、任意の数を持つことができます*プロパティ名*エントリまたは*プロパティ guid*項目と、それぞれ別々 の行にします。

## <a name="entries"></a>エントリ


<a href="" id="property-name"></a>*property-name*  
次のプロパティのいずれかのインスタンスの名前を表す、デバイス[ドライバー パッケージ](driver-packages.md)プロパティ。

-   **DeviceModel**
-   **DeviceVendorWebsite**
-   **DeviceDetailedDescription**
-   **DeviceDocumentationLink**
-   **DeviceIcon**
-   **DeviceBrandingIcon**

<a href="" id="property-category-guid"></a>*property-category-guid*  
プロパティのカテゴリを識別する GUID 値。 GUID 値は、デバイスのインスタンスのプロパティのカテゴリのいずれかを示すシステム定義の GUID を指定できます、[デバイス セットアップ クラス](device-setup-classes.md)、[デバイス インターフェイス クラス](device-interface-classes.md)、またはデバイスのインターフェイス。 同じ GUID 値を持つすべてのプロパティは、同じカテゴリのメンバーです。 これらのプロパティのカテゴリが定義されている*Devpkey.h*します。

GUID 値には、カスタム プロパティのカテゴリを識別する GUID 値をカスタムことができます。

<a href="" id="property-pid"></a>*プロパティの pid*  
プロパティの識別子で示されるプロパティのカテゴリ内の特定のプロパティを示す、*プロパティ カテゴリの guid*値。 内部システム上の理由から、プロパティの識別子が 2 つ以上である必要があります。

<a href="" id="type"></a>型  
数値、10 進数または 16 進数の形式での[プロパティ データ型識別子](https://msdn.microsoft.com/library/windows/hardware/ff541476)プロパティで指定されている、*プロパティ カテゴリの guid*値と*プロパティ pid*値。 次のオプションのみ[**基本データ型**](https://msdn.microsoft.com/library/windows/hardware/ff537793)はサポートされています。

-   DEVPROP_TYPE_STRING
-   DEVPROP_TYPE_STRING_LIST
-   DEVPROP_TYPE_BINARY
-   DEVPROP_TYPE_BOOLEAN
-   DEVPROP_TYPE_UINT32

たとえば、DEVPROP_TYPE_STRING データ型の 10 進数の値は 18 (0x00000012) と DEVPROP_TYPE_STRING_LIST データ型の 10 進値は 2066 (0x00002012)。

<a href="" id="flags"></a>*フラグ*  
オプションに 16 進数の値は、次の追加操作を制御するフラグのビットごとの OR:

<a href="" id="0x00000001--flg-addproperty-noclobber--"></a>**0x00000001** (FLG_ADDPROPERTY_NOCLOBBER)   
値エントリの値が既存のプロパティ値を置換することを防止するフラグ。 ドライバー開発者がプロパティをオーバーライドすることを加えるかどうか**Include**と**必要がある**ディレクティブ、ライターは、そのプロパティには、このフラグを指定する必要があります。 これは、Windows によって参照されている INF セクションを処理するため**Include**と**必要がある**ディレクティブ、を含むINFセクション内の他のすべてのディレクティブを処理した後Windows**Include**と**必要がある**ディレクティブ。

<a href="" id="0x00000002--flg-addproperty-overwriteonly--"></a>**0x00000002** (FLG_ADDPROPERTY_OVERWRITEONLY)   
指定したプロパティが既に存在する場合にのみ、値のエントリの値にプロパティ値を設定するフラグ。

<a href="" id="0x00000004--flg-addproperty-append--"></a>**0x00000004** (FLG_ADDPROPERTY_APPEND)   
既存のプロパティの値のエントリの値に追加されるフラグは文字列値です。 このフラグは、プロパティのデータ型が DEVPROP_TYPE_STRING_LIST である場合にのみ有効です。 指定された文字列は、指定された文字列が既に既存の文字列値である場合、既存のプロパティの文字列値には追加されません。

<a href="" id="0x00000008--flg-addproperty-or-"></a>**0x00000008** (FLG_ADDPROPERTY_OR)  
既存のプロパティ値の値のエントリの値のビットごとの OR を実行するフラグ。 このフラグは、プロパティのデータ型が DEVPROP_TYPE_UINT32 である場合にのみ有効です。

<a href="" id="0x00000010--flg-addproperty-and-"></a>**0x00000010** (FLG_ADDPROPERTY_AND)  
既存のプロパティ値の値のエントリの値のビットごとの AND を実行するフラグ。 このフラグは、プロパティのデータ型が DEVPROP_TYPE_UINT32 である場合にのみ有効です。

<a href="" id="value"></a>*値*  
追加操作を使用してプロパティのデータ型との値によって、プロパティの値を変更する値、*フラグ*エントリ。

<a name="remarks"></a>注釈
-------

**AddProperty**ディレクティブを使用して、デバイスのシステム定義プロパティ、またはカスタムのデバイス プロパティを変更することができます。 このディレクティブは、上記の正式な構文のステートメントで次のセクションのいずれかで指定できます。

各*追加プロパティ セクション*名は、INF ファイル内で一意である必要がありますが、1 つ以上のセクションを参照できます**AddProperty**同じ INF ファイルでディレクティブ。 各セクション名が記載されているセクション名を定義する一般的な規則に従う必要があります[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

詳細については、INF を使用する方法についての**AddProperty**ディレクティブを参照してください[INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)します。

<a name="examples"></a>例
--------

追加のプロパティ セクションの次の例には、2 つの行エントリが含まれています。 最初の行エントリのセット、 **DeviceModel**プロパティ名、および 2 番目の行エントリをカスタム プロパティ キー GUID を指定することによってカスタム デバイス プロパティを設定します。

最初の行が含まれています、*プロパティ名*エントリの値"DeviceModel"および*値*エントリの値「サンプル デバイス モデル名」。

2 番目の行エントリは、カスタム プロパティのカテゴリのカスタム プロパティを設定します。 プロパティのカテゴリの guid エントリの値は"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"とプロパティ識別子のエントリの値は「2」です。

省略可能な*フラグ*エントリの値が存在しないと、型エントリの値が「18」(DEVPROP_TYPE_STRING)。 値のエントリの値は「プロパティが 1 の文字列値」

```ini
[SampleAddPropertySection]
DeviceModel,,,,"Sample Device Model Name"
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 18,, "String value for property 1"
```

## <a name="see-also"></a>関連項目


[**DelProperty**](inf-delproperty-directive.md)

 

 






