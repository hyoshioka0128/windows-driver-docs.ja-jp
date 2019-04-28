---
title: INF Models セクション
description: モデルのセクションのデバイスを識別するには、その DDInstall セクションを参照およびデバイスのハードウェア識別子を指定します。
ms.assetid: b870e8fb-21b4-439b-b858-c45bf9be2ec1
keywords:
- INF モデル セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Models Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3f67c559898f2126af1024f2ae095bcfd5130a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360601"
---
# <a name="inf-models-section"></a>INF Models セクション


製造元ごと*モデル*セクション参照を少なくとも 1 つのデバイスを識別する、 *DDInstall* 、そのデバイスの INF ファイルのセクションを一意に-、-モデルのセクションを指定して[ハードウェア識別子 (ID)](hardware-ids.md)デバイスにします。

任意のエントリの製造元で*モデル*セクションでは 1 つ指定できますもまたはモデルの場合、デバイスと互換性があるその他のデバイス Id が最初のハードウェア ID で指定され、同じドライバーによって制御されます。

```ini
[models-section-name] |
[models-section-name.TargetOSVersion]  (Windows XP and later versions of Windows)

device-description=install-section-name[,hw-id][,compatible-id...]
[device-description=install-section-name[,hw-id][,compatible-id]...] ...
```

## <a name="entries"></a>エントリ


<a href="" id="device-description"></a>*デバイスの説明*  
インストールするのには、デバイスを識別する、文字の表示などの一意の組み合わせで表される、 **%** <em>strkey</em> **%** トークンが定義されています。[ **INF 文字列セクション**](inf-strings-section.md)します。 デバイスの説明の文字の最大長は、LINE_LEN です。

<a href="" id="install-section-name"></a>*install-section-name*  
デバイス (および存在する場合は、デバイスの互換性のあるモデル) に使用する INF インストール セクションの非装飾名を指定します。 詳細については、次を参照してください。 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md)します。

<a href="" id="hw-id"></a>*ハードウェア id*  
ベンダー定義を指定します。[ハードウェア ID](hardware-ids.md) PnP マネージャーはこのデバイスの INF ファイルと一致するものを使用してデバイスを識別する文字列。 このようなハードウェア ID では、次の形式のいずれかがあります。

<a href="" id="enumerator-enumerator-specific-device-id"></a>*列挙子\\列挙子特定のデバイス id*  
1 つの列挙子によって PnP マネージャーに報告された個々 の PnP デバイスの一般的な形式です。 たとえば、 `USB\VID_045E&PID_00B` USB バスで Microsoft HID キーボード デバイスを識別します。 列挙子に応じて、このような仕様を含めることも、デバイスのハードウェアのリビジョン番号として、たとえば、`PCI\VEN_1011&DEV_002&SUBSYS_00000000&REV_02`します。

<a href="" id="-enumerator-specific-device-id"></a>*\*列挙子特定のデバイス id*  
アスタリスクが付いたことを示します (\*) デバイスが 1 つ以上の列挙子でサポートされています。 たとえば、 `*PNP0F01` Microsoft シリアル マウスには、互換性のある id 仕様を持つ識別の`SERENUM\PNP0F01`します。

<a href="" id="device-class-specific-id"></a>*デバイス クラス固有 ID*  
その種類の I/O バス上のすべての周辺機器デバイスのハードウェア Id のバスのハードウェアの仕様」の説明に従って、I/O バス固有形式、です。

1 つ以上を 1 つのデバイスであることができますに注意してください*hw id*値。 PnP マネージャーを使用してこれらの各*hw id*値で、レジストリでこのような各デバイスのサブキーを作成する、その子のデバイスを列挙したときに基になるバスによって通常提供される**Enum**分岐します。 システムのセットアップ コードを使用して手動でインストールされているデバイスの場合、 *hw id*このような各レジストリ サブキーを作成する、対応する INF ファイルで指定された値します。

<a href="" id="compatible-id"></a>*互換性のある id*  
ベンダー定義を指定します。[互換性 ID](compatible-ids.md)互換性のあるデバイスを識別する文字列。 任意の数の*互換性のある id*内のエントリの値を指定することができます、*モデル* セクションで、それぞれ、次へ からをコンマで区切って (**、**)。 このようなすべての互換性のあるデバイスやデバイス モデルは、初期によって指定されたデバイスと同じドライバーによって制御される*hw id*します。

<a name="remarks"></a>コメント
-------

各*モデル セクション名*記載する必要があります、 [ **INF 製造元セクション**](inf-manufacturer-section.md)の INF ファイル。 すべてあたり-の製造元で 1 つまたは複数のエントリが発生できる*モデル*INF ファイルを特定の製造元のインストール数のデバイス (とドライバー) に応じて、セクション。

各*インストール セクション名*INF ファイル内で一意である必要があり、で説明されている、セクション名を定義する一般的な規則に従う必要があります[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。 [ ***DDInstall*** ](inf-ddinstall-section.md)あたり製造元で参照されているセクション名*モデル*セクションに追加の拡張機能を持つことも、指定された*インストール セクション名*ため、追加の定義*DDInstall*セクションでは、特定のデバイスの OS 固有またはプラットフォームに固有のインストール。 クロスプラット フォーム対応のシステム ファイルで拡張機能を使用する方法の詳細については、表示も[INF ファイルを作成する](overview-of-inf-files.md)します。

指定した任意*hw id*または*互換性のある id*で値を指定することも、 [ **INF ControlFlags セクション**](inf-controlflags-section.md)をそのデバイスを防ぐために手動によるインストール中に、エンドユーザーに表示されません。 詳細については*hw id*と*互換性のある id*値を参照してください[識別文字列](device-identification-strings.md)します。

各デバイスおよびドライバーの INF ファイルを使用してインストールされているデバイスのインストーラーがで指定された情報を使用して、 [ **INF 製造元セクション**](inf-manufacturer-section.md)および製造元ごと*モデル*セクションでは、デバイスの説明、製造元の名前、デバイス ID (手動インストールの場合) を生成して、場合によっては、レジストリの互換性リスト値のエントリ。

A*モデル セクション名*含めることができます、 *TargetOSVersion*装飾します。 この装飾の詳細については、次を参照してください。 [ **INF 製造元セクション**](inf-manufacturer-section.md)、具体的には、「解説」セクション。

**重要な**  INF ファイルを装飾する必要があります Windows Server 2003 SP1 以降、*モデル セクション名*、INF でエントリ**製造元** セクションで、関連付けられていると共に、INF*モデル*セクション名、 **.ntia64**または **.ntamd64** x86 以外を指定するプラットフォームの拡張機能は、オペレーティング システムのバージョンを対象します。 X86 ベースのターゲット オペレーティング システムのバージョンの INF ファイルまたは (x64 ベースのアーキテクチャのファイル システム ドライバー INF ファイル) などの非 PnP ドライバーの INF ファイルでは、これらのプラットフォーム拡張機能は必要はありません。 内の各エントリを*モデル*セクションとも呼ばれます、*ドライバー ノード*します。

 

<a name="examples"></a>使用例
--------

この例の製造元ごと*モデル*セクションからシステム マウス クラス インストーラーの INF ファイルでは、いくつかの代表的なエントリを定義する、 [ ***DDInstall*** ](inf-ddinstall-section.md)一部のデバイス/モデルのセクションでします。

```ini
[Manufacturer]
%StdMfg%    =StdMfg         ; (Standard types)
%MSMfg%     =MSMfg          ; Microsoft
; ... %otherMfg% omitted here

[StdMfg]  ; per-Manufacturer Models section 
  ; Std serial mouse
%*pnp0f0c.DeviceDesc%= Ser_Inst,*PNP0F0C,SERENUM\PNP0F0C,SERIAL_MOUSE
  ; Std InPort mouse
%*pnp0f0d.DeviceDesc%      = Inp_Inst,*PNP0F0D
; ... more StdMfg entries 
```

## <a name="see-also"></a>関連項目


[**ControlFlags**](inf-controlflags-section.md)

[***DDInstall***](inf-ddinstall-section.md)

[**製造元**](inf-manufacturer-section.md)

[**文字列**](inf-strings-section.md)

 

 






