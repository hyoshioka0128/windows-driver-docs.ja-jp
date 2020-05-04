---
title: INF BitReg ディレクティブ
description: BitReg ディレクティブは、レジストリの既存の[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値エントリ内のビットを設定またはクリアするために使用される、1つまたは複数の INF ライターで定義されたセクションを参照します。 ただし、このディレクティブは、デバイスやドライバーの INF ファイルではほとんど使用されません。
ms.assetid: d9dc601a-e0bb-488f-8bed-221ad600a88c
keywords:
- INF BitReg ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF BitReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6a26d115323daef1f0a175c7f3dca5945fe8ce6
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223274"
---
# <a name="inf-bitreg-directive"></a>INF BitReg ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Bitreg**ディレクティブは、レジストリの既存の[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値エントリ内のビットを設定またはクリアするために使用される、1つまたは複数の INF ライターで定義されたセクションを参照します。 ただし、このディレクティブは、デバイスやドライバーの INF ファイルではほとんど使用されません。

```inf
[DDInstall] | 
[DDInstall.HW] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)


 
BitReg=bit-registry-section[,bit-registry-section]...
```

**Bitreg**ディレクティブは、上記の正式な構文ステートメントに示されているいずれかのセクションの下で指定できます。 このディレクティブは、次の INF ライターで定義されたセクションのいずれかで指定することもできます。

-   DDInstall. Services セクションで[**Addservice**](inf-addservice-directive.md)ディレクティブによって参照される、*サービスのインストール*セクションまたは*イベントログのインストール*セクション。
-   Ddinstall * で[**addinterface**](inf-addinterface-directive.md)ディレクティブによって参照される*インターフェイスセクション*。 [ *インターフェイス](inf-ddinstall-interfaces-section.md)セクション。
-   [**InterfaceInstall32**](inf-interfaceinstall32-section.md)セクションで参照される*インストールインターフェイスセクション*

**Bitreg**ディレクティブによって参照される名前付きセクションには、次の形式があります。

```inf
[bit-registry-section]
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
...
```

*ビットレジストリセクション*には、任意の数のエントリを含めることができます。各エントリは個別の行にあります。

## <a name="entries"></a>エントリ


<a href="" id="reg-root"></a>*reg-ルート*  
このエントリに指定されている他の値のレジストリツリーのルートを識別します。 値は次のいずれかになります。

<a href="" id="hkcr"></a>**HKCR**  
**HKEY_CLASSES_ROOT**の省略形。

<a href="" id="hkcu"></a>**HKCU**  
**HKEY_CURRENT_USER**の省略形。

<a href="" id="hklm"></a>**HKLM**  
**HKEY_LOCAL_MACHINE**の省略形。

<a href="" id="hku"></a>**HKU**  
**HKEY_USERS**の省略形。

<a href="" id="hkr"></a>**HKR**  
相対ルート: つまり、この省略形を使用して指定されたキーは、次の表に示すように、この**Bitreg**ディレクティブが表示される INF セクションに関連付けられているレジストリキーに対する相対値です。

| BitReg ディレクティブを含む INF セクション                                    | HKR によって参照されるレジストリキー                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***Ddinstall*** |
| INF ***Ddinstall *。HW** |
| INF [ *ddinstall *。Service](inf-ddinstall-services-section.md)s セクション | **サービス**キー                                                                  |

 

**注**  **HKR**は、INF [***DefaultInstall***](inf-defaultinstall-section.md)セクションから参照されるビットレジストリセクションでは使用できません。

 

**HKEY_LOCAL_MACHINE**ルートの下に格納されているドライバー情報の詳細については、「[デバイスとドライバーのレジストリツリーとキー](registry-trees-and-keys.md)」を参照してください。

<a href="" id="subkey"></a>*サブキー*  
この省略可能な値は、INF の[**Strings**](inf-strings-section.md)セクションで定義された%*strkey*% token として、または指定された*reg ルート*(*\\key1\\key2 key3*...) の下のレジストリパスとして表現され、変更する値のエントリを含むキーを指定します。

<a href="" id="value-entry-name"></a>*値-エントリ名*  
変更する (既存の) サブキーの既存の[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値エントリの名前を指定します。 これは、"*引用符で囲ま*れた文字列" として、または INF の [[**文字列**](inf-strings-section.md)] セクションで定義されている%*strkey*% token として表すことができます。

<a href="" id="flags"></a>*示す*  
この省略可能な16進値は、システム定義の下位ワードと上位のフラグ値のビットごとのビットマスクとして表現され、指定したバイトマスクで指定されたビットをクリアするか設定するかを指定します。 既定値は0です。これにより、レジストリの64ビットセクションのビットがクリアされます。

これらの各フラグのビットマスク値は次のとおりです。

<a href="" id="0x00000000--flg-bitreg-clearbits-"></a>**0x00000000** (FLG_BITREG_CLEARBITS)  
*バイトマスク*によって指定されたビットをクリアします。

<a href="" id="0x00000001--flg-bitreg-setbits-"></a>**0x00000001** (FLG_BITREG_SETBITS)  
*バイトマスク*によって指定されたビットを設定します。

<a href="" id="0x00004000---flg-bitreg-32bitkey--"></a>**0x00004000** (FLG_BITREG_32BITKEY)   
(Windows XP 以降のバージョンの Windows)。32ビットレジストリで、指定された変更を行います。 指定しない場合、ネイティブレジストリに変更が加えられます。

<a href="" id="byte-mask"></a>*バイトマスク*  
このバイトサイズのマスクは、16進表記で表され、指定された*値のエントリ名*の現在の値でクリアまたは設定するビットを指定します。

<a href="" id="byte-to-modify"></a>*バイト間の変更*  
このバイトサイズの値 (10 進数で表される) は、変更する[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値内のバイトの0から始まるインデックスを指定します。

<a name="remarks"></a>解説
-------

各*ビットレジストリセクション*名は inf ファイルに対して一意である必要がありますが、同じ inf の他のセクションの**bitreg**ディレクティブで参照できます。 各 INF ライターで作成されたセクション名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

既存の[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値のエントリの値は、INF ファイル内の他の場所にある [レジストリの追加] セクションでその現在の値を上書きすることによって変更することもできます。 レジストリの追加に関するセクションの詳細については、 [**AddReg**](inf-addreg-directive.md)ディレクティブのリファレンスを参照してください。

**Bitreg**ディレクティブを使用するには、別の INF ファイルセクションの定義が必要です。 ただし、このようなセクションでは、既存の[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)型の値のエントリの値をビット単位で変更できます。これにより、残りのすべてのビットの値が保持されます。

<a name="examples"></a>例
--------

次の例は、架空のアプリケーションのビットレジストリセクションを示しています。

```inf
[AppX_BitReg]
; set first bit of byte 0 in ProgramData value entry
HKLM,Software\AppX,ProgramData,1,0x01,0 
; preceding would change value 30,00,10 to 31,00,10

; clear high bit of byte 2 in ProgramData value entry
HKLM,Software\AppX,ProgramData,,0x80,2
; preceding would change value 30,00,f0 to 30,00,70

; set second and third bits of byte 1 in ProgramData value entry
HKLM,Software\AppX,ProgramData,1,0x06,1
; preceding would change value 30,00,f0 to 30,06,f0
```

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**AddReg**](inf-addreg-directive.md)

[**AddService**](inf-addservice-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

 

 






