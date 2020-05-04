---
title: INF DelReg ディレクティブ
description: DelReg ディレクティブは、レジストリから削除するキーや値のエントリを記述する1つ以上の INF ライターで定義されたセクションを参照します。
ms.assetid: a456327f-9b2c-42e6-a575-47ad788aa8b1
keywords:
- INF DelReg ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c929a0d61dbf14eca0cb8fa27af2643127fe9cc3
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223182"
---
# <a name="inf-delreg-directive"></a>INF DelReg ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Delreg**ディレクティブは、レジストリから削除するキーや値のエントリを記述する1つ以上の INF ライターで定義されたセクションを参照します。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows)

 
DelReg=del-registry-section[,del-registry-section]...
```

**Delreg**ディレクティブによって参照される各*del-registry セクション*には、次の形式があります。

```inf
[del-registry-section]
reg-root-string,subkey[,value-entry-name][,flags][,value]
reg-root-string,subkey[,value-entry-name][,flags][,value]
...
```

*Del レジストリセクション*には、任意の数のエントリを含めることができます。各エントリは個別の行にあります。

## <a name="entries"></a>エントリ


<a href="" id="reg-root-string"></a>*reg-root 文字列*  
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
相対ルート。この省略形を使用して指定されたキーは、次の表に示すように、この**Delreg**ディレクティブが表示される INF セクションに関連付けられているレジストリキーを基準としています。

| AddReg ディレクティブを含む NF Section                                     | HKR によって参照されるレジストリキー                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***Ddinstall*** |
| INF ***Ddinstall *。HW** |
| INF [ *ddinstall *。サービス](inf-ddinstall-services-section.md)セクション | **サービス**キー                                                                  |

 

**注**  **Hkr**は、 [**INF DefaultInstall セクション**](inf-defaultinstall-section.md)から参照される*del レジストリセクション*では使用できません。

 

**HKEY_LOCAL_MACHINE**ルートの下に格納されているドライバー情報の詳細については、「[デバイスとドライバーのレジストリツリーとキー](registry-trees-and-keys.md)」を参照してください。

<a href="" id="subkey"></a>*サブキー*  
この省略可能な値は、INF の[**Strings**](inf-strings-section.md)セクションで定義された%*strkey*% token として、または指定された*reg ルート*(<em>key1</em>**\\**<em>key2</em>**\\**<em>key3</em>...) の下のレジストリパスとして、次のいずれかを指定します。

-   指定されたレジストリパスの最後にあるレジストリから削除されるサブキー
-   指定されたエントリ名の削除元となる既存のサブキー

<a href="" id="value-entry-name"></a>*値-エントリ名*  
この値は、指定されたサブキーから削除される名前付きの値のエントリを識別します。 サブキー自体がレジストリから削除されている場合は、この値とその前のコンマを省略する必要があります。

<a href="" id="flags"></a>*示す*  
(Windows XP 以降のバージョンの Windows)。この省略可能な16進値は、システム定義の小さい単語と大きい単語のフラグ値のビットマスクとして表現されるか、値エントリのデータ型を定義するか、またはレジストリ削除操作を制御します。 *フラグ*が指定されていない場合は、*値-エントリ名*(指定されている場合) または*サブキー*が削除されます。

これらの各フラグのビットマスク値は次のとおりです。

<a href="" id="0x00002000--flg-delreg-keyonly-common---"></a>**0x00002000** (FLG_DELREG_KEYONLY_COMMON)   
サブキー全体を削除します。

<a href="" id="0x00004000---flg-delreg-32bitkey-"></a>**0x00004000** (FLG_DELREG_32BITKEY)  
32ビットレジストリで、指定された変更を行います。 指定しない場合、ネイティブレジストリに変更が加えられます。

<a href="" id="0x00018002--flg-delreg-multi-sz-delstring-"></a>**0x00018002** (FLG_DELREG_MULTI_SZ_DELSTRING)  
値によって指定された文字列値に一致する文字列をすべて削除します。 Case は無視されます。

<a href="" id="value"></a>*value*  
(Windows XP 以降のバージョンの Windows)。レジストリ値が必要であることを*フラグ*が示す場合は、レジストリ値を指定します。

<a name="remarks"></a>解説
-------

**Delreg**ディレクティブは、上記の仮構文ステートメントに示されているいずれかのセクションの下で指定できます。 このディレクティブは、次の INF ライターで定義されたセクションのいずれかで指定することもできます。

-   INF Ddinstall で[**addservice**](inf-addservice-directive.md)ディレクティブによって参照される、*サービスのインストール*セクションまたは*イベントログのインストール*セクション[**。 *DDInstall*サービスセクション**](inf-ddinstall-services-section.md)。
-   INF Ddinstall で[**addinterface**](inf-addinterface-directive.md)ディレクティブによって参照される、*インターフェイスの追加セクション* [** *DDInstall*。インターフェイスセクション**](inf-ddinstall-interfaces-section.md)。
-   [**INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)で参照される*インストールインターフェイスセクション*。

一般に、システムコンポーネントまたは他のデバイスの INF ファイルによって設定された既存のサブキー内のサブキーまたは値エントリの削除は、INF では行わないでください。 *削除レジストリセクション*の目的は、同じプロバイダーによって提供される新しい INF ファイルを使用して、以前のインストールから古いレジストリ情報をクリーンアップすることです。

各*del レジストリセクション*名は inf ファイルに対して一意である必要がありますが、同じ inf の他のセクションの**delreg**ディレクティブで参照できます。 各セクション名は、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

Windows XP より前のバージョンのオペレーティングシステムでは、キーを削除する唯一の方法は、次のように指定することです。

```inf
reg-root-string, subkey
```

Windows XP 以降のバージョンの Windows では、次のことも許可されます (32 ビットレジストリを指定する場合)。

```inf
reg-root-string, subkey,,0x4000
```

<a name="examples"></a>例
--------

この例では、システム指定の COM/LPT ポートクラスインストーラーの INF が、COM ポートに関する古い NT 固有のレジストリ情報をレジストリから削除する方法を示します。

```inf
[ComPort.NT]
CopyFiles=ComPort.NT.Copy
AddReg=ComPort.AddReg, ComPort.NT.AddReg
 ... ; more directives omitted here

[ComPort.NT.HW]
DelReg=ComPort.NT.HW.DelReg

[ComPort.NT.Copy]
serial.sys
serenum.sys

[Comport.NT.AddReg]
HKR,,EnumPropPages32,,"MSPorts.dll,SerialPortPropPageProvider"

[ComPort.NT.HW.DelReg]
HKR,,UpperFilters
```

## <a name="see-also"></a>関連項目


[**AddReg**](inf-addreg-directive.md)

[**AddInterface**](inf-addinterface-directive.md)

[**AddService**](inf-addservice-directive.md)

[**BitReg**](inf-bitreg-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。サーヴィス**](inf-ddinstall-services-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**文字列**](inf-strings-section.md)

 

 






