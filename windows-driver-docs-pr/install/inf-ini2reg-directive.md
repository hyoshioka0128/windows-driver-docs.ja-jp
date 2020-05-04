---
title: INF Ini2Reg ディレクティブ
description: Ini2Reg ディレクティブは、指定された INI ファイルの行またはセクションがレジストリに移動される1つ以上の名前付きセクションを参照します。 これにより、指定されたキーの下に1つ以上の値エントリが作成または置換されます。
ms.assetid: 82c7ffb5-7e49-4256-b10a-d7be5df2336a
keywords:
- INF Ini2Reg ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Ini2Reg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45c9d90b7beac0e813b27722e59b4c81b94012dd
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223286"
---
# <a name="inf-ini2reg-directive"></a>INF Ini2Reg ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Ini2Reg**ディレクティブは、指定された INI ファイルの行またはセクションがレジストリに移動される1つ以上の名前付きセクションを参照します。 これにより、指定されたキーの下に1つ以上の値エントリが作成または置換されます。

```inf
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

**Ini2Reg**ディレクティブによって参照される名前付きセクションには、次の形式があります。

```inf
[ini-to-registry-section]
 
ini-file,ini-section,[ini-key],reg-root,subkey[,flags]
...
```

*Ini からレジストリへのセクション*には、任意の数のエントリ (それぞれ別の行) を指定できます。

## <a name="entries"></a>エントリ


<a href="" id="ini-file"></a>*ini-ファイル*  
ソースメディアで提供される INI ファイルの名前を指定します。 この値は、*ファイル名*として、または INF ファイルの[**文字列**](inf-strings-section.md)セクションで定義されている%*strkey*% token として表すことができます。

<a href="" id="ini-section"></a>*ini-セクション*  
コピーするレジストリ情報を含む、指定した INI ファイル内のセクションの名前を指定します。

<a href="" id="ini-key"></a>*ini-キー*  
レジストリにコピーする INI ファイル内のキーの名前を指定します。 この値を省略した場合、 *ini セクション*全体が指定されたレジストリ*サブキー*に転送されます。

<a href="" id="reg-root"></a>*reg-ルート*  
このエントリに指定されている他の値のレジストリツリーのルートを識別します。 詳細については、 [**AddReg ディレクティブ**](inf-addreg-directive.md)のリファレンスを参照してください。

<a href="" id="subkey"></a>*サブキー*  
値を受け取るサブキーを識別します。これは、INF の[**文字列**](inf-strings-section.md)セクションで定義された%*strkey*% トークン、または指定された*reg ルート*からの明示的なレジストリパス (<em>key1</em>**\\**<em>key2</em>**\\**<em>key3</em>...) として表現されます。

<a href="" id="flags"></a>*示す*  
次のように、指定された情報をレジストリに転送した後、またはビット1で既存のレジストリ情報を上書きするかどうかにかかわらず、INI ファイルを処理する方法をビット0で指定します。

<a href="" id="bit-zero---0"></a>ビットゼロ = **0**  
指定された情報をレジストリにコピーした後は、INI ファイルから削除しないでください。 既定値です。

<a href="" id="bit-zero---1"></a>ビットゼロ = **1**  
指定された情報をレジストリに移動した後、INI ファイルから削除します。

<a href="" id="bit-one---0"></a>ビット 1 = **0**  
指定したサブキーがレジストリに既に存在する場合は、INI によって指定された情報をこの*サブキー*に転送しないでください。 それ以外の場合は、この INI が指定した情報を値のエントリとして使用して、指定された*サブキー*をレジストリに作成します。 既定値です。

<a href="" id="bit-one---1"></a>ビット 1 = **1**  
指定したサブキーがレジストリに既に存在する場合は、その値のエントリを INI によって指定された情報に置き換えます。

<a name="remarks"></a>解説
-------

**Ini2Reg**ディレクティブは、正式な構文ステートメントに示されているいずれかのセクションで有効です。 このディレクティブは、 [**Addinterface**](inf-addinterface-directive.md)ディレクティブによって参照されるか、 [**InterfaceInstall32**](inf-interfaceinstall32-section.md)セクションで参照される、INF ライターで定義されたセクションでも有効です。

Windows XP 以降のバージョンの Windows にデバイスをインストールするために INF ファイルが使用されている場合、INF ファイルに**Ini2Reg**ディレクティブを含めることはできません。 **Ini2Reg**ディレクティブが含まれている INF ファイルは、 ["Windows 用に設計" のロゴテスト](https://docs.microsoft.com/windows-hardware/drivers)に合格しません。デジタル署名を受信せず、windows によって信頼されないことになります (「 [Windows がドライバーを選択する方法](how-setup-selects-drivers.md)」を参照してください)。

各 *.ini-レジストリセクション*名は、INF ファイルに対して一意である必要があります。 各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

INF は、次のいずれかの方法で、配布メディアに指定された*ini ファイル*の完全なパスを提供します。

-   IHV/OEM が提供する INF ファイルで、この INF の[**Sourcedisksnames**](inf-sourcedisksnames-section.md)セクションと (場合によっては) [**Sourcedisksnames**](inf-sourcedisksfiles-section.md)セクションを使用して、配布メディアのルートディレクトリ (またはディレクトリ) にない各名前付きソースファイルの完全パスを明示的に指定します。
-   システムが提供する INF ファイルで、1つまたは複数の追加の INF ファイルを指定します。これは、INF ファイルの[**バージョン**](inf-version-section.md)セクションにある**layoutfile**エントリで確認できます。

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**SourceDisksFiles**](inf-sourcedisksfiles-section.md)

[**SourceDisksNames**](inf-sourcedisksnames-section.md)

[**文字列**](inf-strings-section.md)

[**UpdateIniFields**](inf-updateinifields-directive.md)

[**UpdateInis**](inf-updateinis-directive.md)

[**バージョン**](inf-version-section.md)

 

 






