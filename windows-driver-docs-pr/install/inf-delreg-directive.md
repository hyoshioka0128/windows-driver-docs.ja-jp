---
title: INF DelReg ディレクティブ
description: ディレクティブは、1 つまたは複数 INF ライター定義について説明するセクションのキーまたはレジストリから削除する値のエントリを参照します。
ms.assetid: a456327f-9b2c-42e6-a575-47ad788aa8b1
keywords:
- INF してディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbde52ab47f5eb3f99f5f3bf83103c674125d41a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358812"
---
# <a name="inf-delreg-directive"></a>INF DelReg ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A**して**ディレクティブが 1 つまたは複数 INF ライター定義について説明するセクションのキーまたはレジストリから削除する値のエントリを参照します。

```ini
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

各*del-section レジストリ*によって参照される、**して**ディレクティブは、次の形式。

```ini
[del-registry-section]
reg-root-string,subkey[,value-entry-name][,flags][,value]
reg-root-string,subkey[,value-entry-name][,flags][,value]
...
```

A *del-section レジストリ*それぞれ別々 の行に任意の数のエントリを持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="reg-root-string"></a>*reg-root-string*  
このエントリで指定されたその他の値のレジストリ ツリーのルートを識別します。 値は次のいずれかになります。

<a href="" id="hkcr"></a>**HKCR**  
省略形**HKEY_CLASSES_ROOT**します。

<a href="" id="hkcu"></a>**HKCU**  
省略形**HKEY_CURRENT_USER**します。

<a href="" id="hklm"></a>**HKLM**  
省略形**HKEY_LOCAL_MACHINE**します。

<a href="" id="hku"></a>**HKU**  
省略形**HKEY_USERS**します。

<a href="" id="hkr"></a>**HKR**  
この省略形を使用して指定されているキーがこの INF セクションに関連付けられたレジストリ キーを基準との相対のルート**して**ディレクティブが表示されたら、次の表に記載されています。

| %NF セクションを含む AddReg ディレクティブ                                     | HKR によって参照されるレジストリ キー                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***DDInstall*** |
| INF ***DDInstall *。ハードウェア** |
| INF [ * **DDInstall *。サービス**](inf-ddinstall-services-section.md)セクション | **サービス**キー                                                                  |

 

**注**  **HKR**では使用できません、 *del-section レジストリ*から参照されている、 [ **INF DefaultInstall セクション**](inf-defaultinstall-section.md)します。

 

下に格納されているドライバー情報の詳細については、 **HKEY_LOCAL_MACHINE**ルートは、「[レジストリ ツリーとデバイスとドライバーのキー](registry-trees-and-keys.md)します。

<a href="" id="subkey"></a>*サブキー*  
このオプションの値の形式を % として*strkey*% のトークンで定義されている、 [**文字列**](inf-strings-section.md)セクション、INF または下のレジストリ パスとして、指定された*reg ルート*(<em>key1</em>**\\**<em>key2</em>**\\**<em>key3</em>...)、次のいずれかを指定します。

-   指定されたレジストリ パスの最後に、レジストリから削除するサブキー
-   元の特定値のエントリの名前は削除するのには、既存のサブキー

<a href="" id="value-entry-name"></a>*value-entry-name*  
この値は、指定したサブキーから削除する名前付きの値のエントリを識別します。 レジストリからサブキー自体が削除される場合、この値は、その前のコンマは省略する必要があります。

<a href="" id="flags"></a>*フラグ*  
(Windows XP および Windows の以降のバージョン。)この省略可能な 16 進値、下位ワードのシステム定義の上位ワード フラグの論理和のビットマスク値、値のエントリのデータ型を定義または削除レジストリ操作を制御として表されます。 場合*フラグ*が指定されていない、*値のエントリ名*(選択した場合のみ) または*サブキー*は削除されます。

これらのフラグのビットマスク値は次のとおりです。

<a href="" id="0x00002000--flg-delreg-keyonly-common---"></a>**0x00002000** (FLG_DELREG_KEYONLY_COMMON)   
全体のサブキーを削除します。

<a href="" id="0x00004000---flg-delreg-32bitkey-"></a>**0x00004000** (FLG_DELREG_32BITKEY)  
32 ビットのレジストリで指定された変更を加えます。 指定しない場合は、ネイティブのレジストリに変更が行わします。

<a href="" id="0x00018002--flg-delreg-multi-sz-delstring-"></a>**0x00018002** (FLG_DELREG_MULTI_SZ_DELSTRING)  
複数行文字列レジストリ エントリの値で指定された文字列値に一致するすべての文字列を削除します。 場合は無視されます。

<a href="" id="value"></a>*値*  
(Windows XP および Windows の以降のバージョン。)場合に、レジストリ値を指定します*フラグ*レジストリ値が必要であることを示します。

<a name="remarks"></a>コメント
-------

A**して**上記の正式な構文のステートメントで次のセクションのいずれかのディレクティブを指定できます。 このディレクティブは、INF ライター定義の次のセクションのいずれかも指定できます。

-   A*サービス-インストール セクション*または*インストール ログ イベントが*セクションによって参照される、 [ **AddService** ](inf-addservice-directive.md)ディレクティブで、 [ **INF *DDInstall*します。サービス セクション**](inf-ddinstall-services-section.md)します。
-   *追加インターフェイス セクション*によって参照される、 [ **AddInterface** ](inf-addinterface-directive.md)ディレクティブで、 [ **INF *DDInstall*.インターフェイス セクション**](inf-ddinstall-interfaces-section.md)します。
-   *インストール-section インターフェイス*で参照されている、 [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)します。

一般に、INF では、サブキーまたはシステム コンポーネントによって、またはその他のデバイスの INF ファイルによって設定された既存のサブキー内の値のエントリを削除する試みる必要があることはありません。 目的を*delete レジストリ セクション*同じプロバイダーによって提供される新しい INF ファイルを使用して以前のインストールから古いレジストリ情報をクリーンアップします。

各*del-section レジストリ*名は、INF ファイルに固有である必要がありますが、それを参照できます**して**同じ INF の他のセクション ディレクティブ。 各セクション名は、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

Windows XP より前のオペレーティング システムのバージョンは、キーを削除する唯一の方法は、次を指定することです。

```ini
reg-root-string, subkey
```

Windows XP と Windows の以降のバージョンでは、次を許可 (32 ビット レジストリの指定)。

```ini
reg-root-string, subkey,,0x4000
```

<a name="examples"></a>使用例
--------

この例では、どのシステム提供の COM と LPT ポート クラス インストーラーの INF 削除古い NT 固有レジストリ情報レジストリから COM ポートについてを示します。

```ini
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

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[***DDInstall *。サービス**](inf-ddinstall-services-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**文字列**](inf-strings-section.md)

 

 






