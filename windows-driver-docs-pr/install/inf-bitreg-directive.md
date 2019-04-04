---
title: INF BitReg ディレクティブ
description: BitReg ディレクティブ参照の 1 つまたは複数定義ライター INF セクションまたは内で、既存のビットをオフに設定するために使用[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-レジストリのエントリの値を入力します。 ただし、このディレクティブは、デバイスとドライバーの INF ファイルを使用非常にまれです。
ms.assetid: d9dc601a-e0bb-488f-8bed-221ad600a88c
keywords:
- INF BitReg ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF BitReg Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8085f27eeef0a58f253728384c831e1afd415183
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539643"
---
# <a name="inf-bitreg-directive"></a>INF BitReg ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **BitReg**ディレクティブが 1 つまたは複数定義ライター INF セクションまたは内で、既存のビットをオフに設定するために使用を参照[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-レジストリのエントリの値を入力します。 ただし、このディレクティブは、デバイスとドライバーの INF ファイルを使用非常にまれです。

```ini
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

A **BitReg**上記の正式な構文のステートメントで次のセクションのいずれかのディレクティブを指定できます。 このディレクティブは、INF ライター定義の次のセクションのいずれかも指定できます。

-   A*サービス-インストール セクション*または*インストール ログ イベントが*セクションによって参照される、 [ **AddService** ](inf-addservice-directive.md)ディレクティブで、DDInstall.Services セクション。
-   *追加インターフェイス セクション*によって参照される、 [ **AddInterface** ](inf-addinterface-directive.md)ディレクティブで、 [ * **DDInstall *。インターフェイス**](inf-ddinstall-interfaces-section.md)セクション。
-   *インストール-section インターフェイス*で参照されている、 [ **InterfaceInstall32** ](inf-interfaceinstall32-section.md)セクション

セクションによって参照される各名前付き、 **BitReg**ディレクティブは、次の形式。

```ini
[bit-registry-section]
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
reg-root, [subkey], value-entry-name, [flags], byte-mask, byte-to-modify
...
```

A*ビットのレジストリ セクション*それぞれ別々 の行に任意の数のエントリを持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="reg-root"></a>*レジストリ ルート*  
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
相対ルート − この略語は、この INF セクションに関連付けられたレジストリ キーを使用して指定されているキーは、 **BitReg**ディレクティブが表示されたら、次の表に記載されています。

| INF セクションを含む BitReg ディレクティブ                                    | HKR によって参照されるレジストリ キー                                                        |
|----------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
| INF ***DDInstall*** |
| INF ***DDInstall *。ハードウェア** |
| INF [ * **DDInstall *。サービス**](inf-ddinstall-services-section.md)のセクション | **サービス**キー                                                                  |

 

**注**  **HKR** 、INF から参照のビットのレジストリのセクションでは使用できません[ ***DefaultInstall*** ](inf-defaultinstall-section.md)セクション。

 

下に格納されているドライバー情報の詳細については、 **HKEY_LOCAL_MACHINE**ルートは、「[レジストリ ツリーとデバイスとドライバーのキー](registry-trees-and-keys.md)します。

<a href="" id="subkey"></a>*サブキー*  
このオプションの値で表される % として*strkey*% のトークンで定義されている、 [**文字列**](inf-strings-section.md)セクション、INF または下のレジストリ パスとして、指定された*reg ルート* (*key1\\key2\\key3*...) を変更する値のエントリを含むキーを指定します。

<a href="" id="value-entry-name"></a>*value-entry-name*  
既存の名前を示す[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-値のエントリを変更する (既存) のサブキーに入力します。 表現できるとして"*文字列を引用符で囲まれた*"または % として*strkey*INF ので定義されている % トークン[**文字列**](inf-strings-section.md)セクション。

<a href="" id="flags"></a>*フラグ*  
システム定義の下位ワードと上位ワード フラグの値の論理和のビットマスクで表されるこの省略可能な 16 進値では、オフ、または特定のバイト マスクで指定されたビットを設定するかどうかを指定します。 既定値は、0 で、レジストリの 64 ビットのセクション内のビットをクリアします。

これらのフラグのビットマスク値は次のとおりです。

<a href="" id="0x00000000--flg-bitreg-clearbits-"></a>**0x00000000** (FLG_BITREG_CLEARBITS)  
指定されたビットをオフに*バイト マスク*します。

<a href="" id="0x00000001--flg-bitreg-setbits-"></a>**0x00000001** (FLG_BITREG_SETBITS)  
設定で指定されたビット*バイト マスク*します。

<a href="" id="0x00004000---flg-bitreg-32bitkey--"></a>**0x00004000** (FLG_BITREG_32BITKEY)   
(Windows XP および Windows の以降のバージョン。)32 ビットのレジストリで指定された変更を加えます。 指定しない場合は、ネイティブのレジストリに変更が行わします。

<a href="" id="byte-mask"></a>*バイト マスク*  
このバイト サイズ マスク、16 進表記で表されるを指定するビットをオフまたはの現在の値で設定する、指定された*値のエントリ名*します。

<a href="" id="byte-to-modify"></a>*バイトの修正*  
このバイト サイズの値を 10 進数、内のバイトの 0 から始まるインデックスを指定します、 [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-変更する値を入力します。

<a name="remarks"></a>注釈
-------

各*ビットのレジストリ セクション*名は、INF ファイルに固有である必要がありますが、それを参照できます**BitReg**同じ INF の他のセクション ディレクティブ。 各 INF ライター作成セクション名は、INF ファイル内で一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

既存の値[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-INF ファイルで別の場所の追加レジストリ セクション内の現在の値を上書きすることで、型の値のエントリを変更こともできます。 詳細については、レジストリの追加のセクションでは、のリファレンスを参照してください、 [ **AddReg**](inf-addreg-directive.md)ディレクティブ。

使用して、 **BitReg**ディレクティブには、別の INF ファイルのセクションの定義が必要です。 ただし、既存の値[REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-型の値のエントリが変更 - ビットで、このようなセクションですべての残りのビットの値はそのまま維持できます。

<a name="examples"></a>例
--------

次の例では、架空のアプリケーションのビット レジストリ セクションを示します。

```ini
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

[***DDInstall *。共同インストーラー**](inf-ddinstall-coinstallers-section.md)

[***DDInstall *。ハードウェア**](inf-ddinstall-hw-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

 

 






