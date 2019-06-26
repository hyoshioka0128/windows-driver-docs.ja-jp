---
title: INF DelProperty ディレクティブ
description: DelProperty は、デバイス インスタンス、デバイス セットアップ クラスをデバイス インターフェイス クラス、またはデバイス インターフェイスのデバイスのプロパティを削除する INF ファイルのセクションを参照します。
ms.assetid: fff227de-1664-4c9b-8709-1a8e1966bd79
keywords:
- INF DelProperty ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelProperty Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d9c4540e78c1eac8d19eff5a088eb82e9d82678
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365846"
---
# <a name="inf-delproperty-directive"></a>INF DelProperty ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **DelProperty**ディレクティブを削除する 1 つまたは複数の INF ファイルでセクションを参照する[デバイス プロパティ](device-properties.md)デバイス インスタンスの場合、[デバイス セットアップ クラス](device-setup-classes.md)、 [デバイスのインターフェイス クラス](device-interface-classes.md)、またはデバイスのインターフェイス。

```ini
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

A **DelProperty**上記の正式な構文のステートメントで次のセクションのいずれかのディレクティブを指定できます。

A *del-section プロパティ*によって参照される、 **DelProperty**ディレクティブは、次の形式。

```ini
[del-property-section]
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
(property-name [ ,, flags [, value]]) | ({property-category-guid}, property-pid [ , flags [, value]])
...
```

A *del-section プロパティ*の任意の数を持つことができます*プロパティ名*エントリまたは*プロパティ guid*項目と、それぞれ別々 の行にします。

## <a name="entries"></a>エントリ


<a href="" id="property-name"></a>*property-name*  
プロパティのいずれかのインスタンスの名前を表す、デバイス[ドライバー パッケージ](driver-packages.md)プロパティ。 サポートされているプロパティ名は、のトピックで説明したものと同じ、*プロパティ名*のエントリ、 [ **INF AddProperty ディレクティブ**](inf-addproperty-directive.md)します。

<a href="" id="property-category-guid"></a>*property-category-guid*  
プロパティのカテゴリを識別する GUID 値。 GUID 値には、システム定義のプロパティのカテゴリを識別するシステム定義の GUID またはカスタムのカスタム プロパティのカテゴリを識別する GUID を指定できます。 サポートされている GUID 値は、の説明にあるものと同じ、*プロパティ カテゴリの guid* 、INF のエントリ[ **AddProperty** ](inf-addproperty-directive.md)ディレクティブ。

<a href="" id="property-pid"></a>*プロパティの pid*  
プロパティの識別子で示されるプロパティのカテゴリ内の特定のプロパティを示す、*プロパティ カテゴリの guid*値。 内部システム上の理由から、プロパティの識別子が 2 つ以上である必要があります。

<a href="" id="flags"></a>*フラグ*  
削除操作を制御する省略可能な 16 進数のフラグ値を指定します。 サポートされる唯一のフラグ値は次のとおりです。

<a href="" id="0x00000001--flg-delproperty-multi-sz-delstring-"></a>**0x00000001** (FLG_DELPROPERTY_MULTI_SZ_DELSTRING)  
プロパティのデータ型の場合[ **DEVPROP_TYPE_STRING_LIST**](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-string-list)、この操作は、既存の文字列リストに値のエントリの値によって指定された文字列に一致するすべての文字列を削除します。 文字の大文字と小文字は、指定された文字列と文字列の一覧で、既存の文字列の比較ではありません。

<a href="" id="value"></a>*値*  
プロパティのデータ型は DEVPROP_TYPE_STRING_LIST いてフラグ エントリが**0x00000001**、*値*エントリの値が一致する文字列で、削除操作を使用して検索する文字列を提供します既存の文字列を一覧表示し、削除操作が既存の文字列の一覧から、一致した文字列を削除する一致する文字列が見つかった場合します。

<a name="remarks"></a>注釈
-------

一般に、システム コンポーネントによって、または別の INF ファイルで設定されているデバイスのプロパティを削除する、INF ファイルを使用する必要がありますされません。 主な目的、 **DelProperty**ディレクティブは、前のデバイスのインストールを更新する INF ファイルで使用して、以前のデバイス インストールの設定されたプロパティは必要なくなりました。

A *del-section プロパティ*名は、INF ファイル内で一意である必要がありますが、1 つ以上のセクション名を参照できます**DelProperty**同じ INF ファイルでディレクティブ。 セクション名が記載されているセクション名を定義する一般的な規則に従う必要があります[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

使用する方法についての詳細、 **DelProperty**ディレクティブを参照してください[INF AddProperty ディレクティブと INF DelProperty ディレクティブを使用して](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)します。

<a name="examples"></a>例
--------

削除のプロパティ セクションの次の例には、2 つの行エントリが含まれています: 行の最初のエントリが含まれています、*プロパティ名*を削除するエントリの値、 **DeviceModel**プロパティ、および 2 番目の行エントリは、データ型が DEVPROP_TYPE_STRING_LIST カスタム デバイス プロパティの値から文字列"DeleteThisString"を削除します。 2 番目の行で、*プロパティ カテゴリの guid*エントリの値は"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e、"、*プロパティ識別子*エントリの値は「2」、および*フラグ*エントリの値は"0x00000001、"

```ini
[SampleDelPropertySection]
DeviceModel
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 0x00000001, "DeleteThisString"
```

## <a name="see-also"></a>関連項目


[**AddProperty**](inf-addproperty-directive.md)

 

 






