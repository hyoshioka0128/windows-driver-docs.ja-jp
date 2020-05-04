---
title: INF DelFiles ディレクティブ
description: DelFiles ディレクティブは、inf ファイル内の他の場所で INF ライターによって定義されたセクションを参照し、ファイルの一覧を削除します。
ms.assetid: e163f88f-e0ab-41e7-97df-49853ec0836f
keywords:
- INF DelFiles ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DelFiles Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b125bff6055f21812249f3b410eec44f21ca0a48
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223108"
---
# <a name="inf-delfiles-directive"></a>INF DelFiles ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Delfiles**ディレクティブは、inf ファイル内の他の場所で inf ライターによって定義されたセクションを参照し、参照している**delfiles**ディレクティブが指定されているセクションの操作のコンテキストでファイルの一覧を削除します。

```inf
[DDInstall] | 
[DDInstall.CoInstallers] | 
[ClassInstall32] | 
[ClassInstall32.ntx86] | 
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  (Windows XP and later versions of Windows) 
[ClassInstall32.ntarm]  (Windows 8 and later versions of Windows) 
[ClassInstall32.ntarm64]  (Windows 10 and later versions of Windows) 


  
Delfiles=file-list-section[,file-list-section]... 
```

**Delfiles**ディレクティブは、正式な構文ステートメントに示されている任意のセクション内で指定できます。 このディレクティブは、次のいずれかの INF ライターで定義されたセクション内で指定することもできます。

-   Ddinstall * で[**addinterface**](inf-addinterface-directive.md)ディレクティブによって参照されるインターフェイスセクション。 [ *インターフェイス](inf-ddinstall-interfaces-section.md)セクション。
-   [**InterfaceInstall32**](inf-interfaceinstall32-section.md)セクションで参照されるインストールインターフェイスセクション

**Delfiles**ディレクティブによって参照される各名前付きセクションには、次の形式の1つ以上のエントリがあります。

```inf
[file-list-section]
 
destination-file-name[,,,flag]
...
```

*ファイルリストセクション*には任意の数のエントリを含めることができ、それぞれが個別の行に表示されます。

## <a name="entries"></a>エントリ


<a href="" id="destination-file-name"></a>*変換先-ファイル名*  
転送先から削除するファイルの名前を指定します。

[**CopyFiles**](inf-copyfiles-directive.md)ディレクティブに示されているファイルを指定しないでください。 [ **CopyFiles**参照] セクションと [ **delfiles**-参照] セクションの両方にファイルが表示され、そのファイルが有効な署名を持つシステムに現在存在している場合、オペレーティングシステムはコピー操作を最適化し、削除操作を実行する可能性があります。 これは、ほとんどの場合、INF ライターが意図したものでは*ありません*。

**メモ**  %*strkey*% トークンを使用して、宛先ファイル名のエントリを指定することはできません。 %*Strkey*% トークンの詳細については、「 [**INF Strings」セクション**](inf-strings-section.md)を参照してください。

 

<a href="" id="flag"></a>*誤り*  
この省略可能な値には、次のいずれかを指定することができます。16進表記では、または10進値として表示されます。

<a href="" id="0x00000001--delflg-in-use-"></a>**0x00000001** (DELFLG_IN_USE)  
名前付きファイルは、インストールプロセス中に使用された後に削除します。

このフラグ値を INF に設定すると、指定されたファイルを削除できない場合に、システムが再起動されるまでファイル削除操作をキューに配置します。このファイルは、この INF の処理中に使用されているためです。 それ以外の場合、このようなファイルは削除されません。

<a href="" id="0x00010000---delflg-in-use1-"></a>**0x00010000** (DELFLG_IN_USE1)  
(Windows 2000 以降のバージョンの Windows)このフラグは DELFLG_IN_USE フラグの上位ワードバージョンであり、同じ目的と効果があります。 このフラグは、NT ベースのシステムでののインストールにのみ使用してください。

INF でこのフラグ値を設定すると、同じ*ファイルリストセクション*を参照する**Delfiles**と[**CopyFiles**](inf-copyfiles-directive.md)ディレクティブの両方を使用した、inf の COPYFLG_WARN_IF_SKIP フラグとの競合を防ぐことができます。

<a name="remarks"></a>解説
-------

**重要**  このディレクティブは、慎重に使用する必要があります。 プラグアンドプレイ (PnP) 関数ドライバーの INF ファイルでは、 **Delfiles**ディレクティブを使用しないことを強くお勧めします。

 

すべての*ファイルリストセクション*名は inf ファイルに対して一意である必要がありますが、同じ inf 内の他の場所では、 [**CopyFiles**](inf-copyfiles-directive.md)、 **Delfiles**、または[**RenFiles**](inf-renfiles-directive.md)ディレクティブで参照できます。 このような INF ライターで定義されたセクション名は、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

**Delfiles**ディレクティブでは、システム定義のプラットフォーム拡張機能 (**. nt**、 **ntx86**、. **ntia64**、. **ntamd64**、 **. ntarm**、または**ntarm64**) を使用した*ファイルリストセクション*名の装飾はサポートされていません。

INF ファイルの[**Destinationdirs**](inf-destinationdirs-section.md)セクションは、特定の**delfiles**ディレクティブを含むセクションに関係なく、すべてのファイル削除操作の対象を制御します。 **Delfiles**ディレクティブによって参照される名前付きセクションに、同じ INF の**destinationdirs**セクションに対応するエントリがある場合、そのエントリは、指定されたセクションに示されているすべてのファイルが削除されるターゲットの宛先ディレクトリを明示的に指定します。 名前付きセクションが**Destinationdirs**セクションに表示されていない場合、WINDOWS は INF の**DefaultDestDir**エントリを使用します。

<a name="examples"></a>例
--------

この例では、簡単なデバイスドライバーの INF を処理するときに実行されるファイル削除操作のパスを[**Destinationdirs**](inf-destinationdirs-section.md)セクションで指定する方法を示します。

```inf
[DestinationDirs]
DefaultDestDir = 12  ; DIRID_DRIVERS 

; ... 

[AHA154X]
CopyFiles=@AHA154x.MPD
DelFiles=ASPIDEV ; defines delete-files section name
; ... some other directives and sections omitted here

[ASPIDEV]
VASPID.SYS ; name of file to be deleted, if it exists on target 
; ...
```

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[**ClassInstall32**](inf-classinstall32-section.md)

[**CopyFiles**](inf-copyfiles-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[***DDInstall *。CoInstallers**](inf-ddinstall-coinstallers-section.md)

[**DestinationDirs**](inf-destinationdirs-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

**RenFiles**
[**文字列**](inf-strings-section.md)

 

 






