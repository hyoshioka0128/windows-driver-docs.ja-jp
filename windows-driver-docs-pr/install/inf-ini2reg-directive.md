---
title: INF Ini2Reg ディレクティブ
description: Ini2Reg ディレクティブでは、レジストリに行または指定された INI ファイルからセクションを移動します。 1 つまたは複数の名前付きセクションを参照します。 これを作成または指定したキーの下で 1 つまたは複数の値のエントリを置き換えます。
ms.assetid: 82c7ffb5-7e49-4256-b10a-d7be5df2336a
keywords:
- INF Ini2Reg ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Ini2Reg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb47ba37497f378082b855452ab8db79f334df3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574356"
---
# <a name="inf-ini2reg-directive"></a>INF Ini2Reg ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

**Ini2Reg**ディレクティブでは、レジストリに行または指定された INI ファイルからセクションを移動します。 1 つまたは複数の名前付きセクションを参照します。 これを作成または指定したキーの下で 1 つまたは複数の値のエントリを置き換えます。

```ini
        [
        DDInstall
        ] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


  
Ini2Reg=ini-to-registry-section[,ini-to-registry-section]...
```

セクションによって参照される各名前付き、 **Ini2Reg**ディレクティブは、次の形式。

```ini
[ini-to-registry-section]
 
ini-file,ini-section,[ini-key],reg-root,subkey[,flags]
...
```

*セクション レジストリ ini* INF ライター決定エントリの数をそれぞれ個別の行に持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="ini-file"></a>*ini ファイル*  
ソース メディアに、INI ファイルの名前を指定します。 としてこの値を表すことが、 *filename*または % として*strkey*% トークンで定義されている、 [**文字列**](inf-strings-section.md) INF ファイルのセクション。

<a href="" id="ini-section"></a>*ini セクション*  
コピーするレジストリ情報が含まれる指定された INI ファイル内のセクションの名前を指定します。

<a href="" id="ini-key"></a>*ini-key*  
INI ファイル、レジストリにコピーするには、キーの名前を指定します。 この値を省略した場合、全体*ini セクション*が指定されたレジストリに転送される*サブキー*します。

<a href="" id="reg-root"></a>*レジストリ ルート*  
このエントリで指定されたその他の値のレジストリ ツリーのルートを識別します。 詳しくは、リファレンスを参照してください、 [ **AddReg ディレクティブ**](inf-addreg-directive.md)します。

<a href="" id="subkey"></a>*サブキー*  
値を受け取るサブキーを指定 % として表される*strkey*% のトークンで定義されている、 [**文字列**](inf-strings-section.md)セクション、INF のか、明示的なレジストリ パス (<em>key1</em>**\\**<em>key2</em>**\\**<em>key3</em>...) から、指定されました。*reg ルート*します。

<a href="" id="flags"></a>*フラグ*  
転送後に指定された情報をレジストリにや (ビット 1) で次のように、既存のレジストリ情報を上書きするかどうか、INI ファイルを処理する方法 (ビット 0) で指定します。

<a href="" id="bit-zero---0"></a>ビット 0 = **0**  
レジストリにコピーした後で、INI ファイルから指定された情報を削除しないでください。 既定値です。

<a href="" id="bit-zero---1"></a>ビット 0 = **1**  
レジストリに移動した後は、INI ファイルから指定された情報を削除します。

<a href="" id="bit-one---0"></a>ビット 1 = **0**  
レジストリで指定したサブキーが既に存在する場合では、これに INI が指定した情報は転送しないで*サブキー*します。 それ以外の場合、指定された作成*サブキー*この INI が指定した情報としてその値のエントリでレジストリにします。 既定値です。

<a href="" id="bit-one---1"></a>ビット 1 = **1**  
レジストリで指定したサブキーが存在する場合は、INI が指定した情報でその値のエントリを置き換えます。

<a name="remarks"></a>コメント
-------

**Ini2Reg**ディレクティブは、正式な構文のステートメントで次のセクションのいずれかで無効です。 このディレクティブは、INF ライター定義のセクションで参照されているは有効ではまた、 [ **AddInterface** ](inf-addinterface-directive.md)ディレクティブまたはで参照されている、 [ **InterfaceInstall32**](inf-interfaceinstall32-section.md)セクション。

INF ファイルにはする必要がありますが含まれていない場合は、INF ファイルを使用するには、Windows XP および以降のバージョンの Windows デバイスをインストールすると、 **Ini2Reg**ディレクティブ。 INF ファイルが含まれている**Ini2Reg**ディレクティブに合格しない["Windows 用に設計されています"のロゴ テスト](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver)、デジタル署名は表示されず、そのため、Windows によって信頼されます (を参照してください[方法Windows ドライバーを選択します。](how-setup-selects-drivers.md))。

各*セクション レジストリ ini*名は、INF ファイルに一意である必要があります。 各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

完全なパスを提供する、INF、指定された*ini ファイル*配布メディアの次のいずれかの。

-   使用して、IHV と OEM 提供の INF ファイルで、 [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)と、おそらく[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)にこの INF セクション配布メディアのルート ディレクトリ (またはディレクトリ) ではない各名前付きのソース ファイルの完全なパスを明示的に指定します。
-   1 つまたは複数追加 INF ファイルで特定の指定した INF システムが指定したファイルの**LayoutFile**内のエントリ、 [**バージョン**](inf-version-section.md) INF ファイルのセクション。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**バージョン**](inf-version-section.md)

 

 






