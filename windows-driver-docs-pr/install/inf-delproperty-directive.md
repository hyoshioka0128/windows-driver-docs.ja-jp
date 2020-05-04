---
title: INF DelProperty ディレクティブ
description: DelProperty は、デバイスインスタンス、デバイスセットアップクラス、デバイスインターフェイスクラス、またはデバイスインターフェイスのデバイスプロパティを削除する INF ファイルセクションを参照します。
ms.assetid: fff227de-1664-4c9b-8709-1a8e1966bd79
keywords:
- INF DelProperty ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelProperty Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45c9dfded0781068b0793c6909bb21e45ac74507
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223186"
---
# <a name="inf-delproperty-directive"></a>INF DelProperty ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Delproperty**ディレクティブは、デバイスインスタンス、[デバイスセットアップクラス](device-setup-classes.md)、[デバイスインターフェイスクラス](device-interface-classes.md)、またはデバイスインターフェイスの[デバイスプロパティ](device-properties.md)を削除する1つ以上の INF ファイルセクションを参照します。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm] |  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64] |  (Windows 10 and later versions of Windows)

[interface-install-section] | 
[interface-install-section.nt] | 
[interface-install-section.ntx86] | 
[interface-install-section.ntia64] |  (Windows XP and later versions of Windows)
[interface-install-section.ntamd64] |  (Windows XP and later versions of Windows)
[interface-install-section.ntarm] |  (Windows 8 and later versions of Windows)
[interface-install-section.ntarm64] |  (Windows 10 and later versions of Windows)


[add-interface-section] 
 
DelProperty=del-property-section[,del-property-section]...  (Windows Vista and later versions of Windows)
```

**Delproperty**ディレクティブは、上記の仮構文ステートメントに示されているいずれかのセクションの下で指定できます。

**Delproperty**ディレクティブによって参照される*del プロパティセクション*の形式は次のとおりです。

```inf
[del-property-section]
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
...
```

*Del プロパティセクション*には、任意の数の*プロパティ名*エントリまたは*プロパティ guid*エントリを含めることができます。それぞれの行は別個の行にあります。

## <a name="entries"></a>エントリ


<a href="" id="property-name"></a>*プロパティ名*  
デバイスインスタンス[ドライバーパッケージ](driver-packages.md)のプロパティを表すプロパティ名の1つ。 サポートされているプロパティ名は、 [**INF AddProperty ディレクティブ**](inf-addproperty-directive.md)の*プロパティ名*のエントリに記述されているものと同じです。

<a href="" id="property-category-guid"></a>*プロパティ-カテゴリ-guid*  
プロパティカテゴリを識別する GUID 値。 GUID 値には、システム定義のプロパティカテゴリを識別するシステム定義の GUID、またはカスタムプロパティカテゴリを識別するカスタム GUID を指定できます。 サポートされている GUID 値は、INF [**Addproperty**](inf-addproperty-directive.md)ディレクティブの*プロパティカテゴリ guid*のエントリに記述されているものと同じです。

<a href="" id="property-pid"></a>*プロパティ-pid*  
プロパティカテゴリ内の特定のプロパティを示すプロパティ識別子。このプロパティは、*カテゴリ guid*値によって示されます。 内部システムの理由により、プロパティ識別子は2以上である必要があります。

<a href="" id="flags"></a>*示す*  
削除操作を制御する省略可能な16進フラグ値。 サポートされているフラグ値は次のとおりです。

<a href="" id="0x00000001--flg-delproperty-multi-sz-delstring-"></a>**0x00000001** (FLG_DELPROPERTY_MULTI_SZ_DELSTRING)  
プロパティのデータ型が[**DEVPROP_TYPE_STRING_LIST**](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string-list)場合、操作は、値のエントリによって指定された文字列に一致する既存の文字列リストを含むすべての文字列を削除します。 指定された文字列と文字列リスト内の既存の文字列の比較では、文字の大文字と小文字は考慮されません。

<a href="" id="value"></a>*value*  
プロパティのデータ型が DEVPROP_TYPE_STRING_LIST で、flags エントリが**0x00000001**の場合、*値*エントリの値は、削除操作が既存の文字列リスト内の一致する文字列を検索するために使用する文字列を指定します。一致する文字列が見つかった場合は、削除操作によって、一致する文字列が既存の文字列リストから削除されます。

<a name="remarks"></a>解説
-------

一般に、システムコンポーネントまたは別の INF ファイルによって設定されたデバイスプロパティの削除には、INF ファイルを使用しないでください。 **Delproperty**ディレクティブの主な目的は、以前のデバイスのインストールを更新する INF ファイルで使用することです。以前のデバイスのインストール用に設定されたプロパティは必要なくなりました。

*Del プロパティセクション*名は inf ファイル内で一意である必要がありますが、同じ inf ファイル内の複数の**delproperty**ディレクティブでセクション名を参照することはできます。 セクション名は、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」で説明されているセクション名を定義するための一般的な規則に従う必要があります。

**Delproperty**ディレクティブの使用方法の詳細については、「 [Inf addproperty ディレクティブと Inf Delproperty ディレクティブの使用](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)」を参照してください。

<a name="examples"></a>例
--------

次の例の delete プロパティセクションには、2つの行エントリが含まれています。最初の行エントリには、 **DeviceModel**プロパティを削除する*プロパティ名*のエントリ値が含まれています。2行目のエントリは、データ型が DEVPROP_TYPE_STRING_LIST であるカスタムデバイスプロパティ値から文字列 "deletethe string" を削除します。 2行目では、*プロパティ-カテゴリ-guid*エントリの値は "c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e" で、*プロパティ識別子*エントリの値は "2" で、 *flags*エントリの値は "0x00000001" です。

```inf
[SampleDelPropertySection]
DeviceModel
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 0x00000001, "DeleteThisString"
```

## <a name="see-also"></a>関連項目


[**AddProperty**](inf-addproperty-directive.md)

 

 






