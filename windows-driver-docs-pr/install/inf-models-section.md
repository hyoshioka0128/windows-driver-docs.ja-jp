---
title: INF Models セクション
description: モデルセクションは、デバイスを識別し、その DDInstall セクションを参照し、デバイスのハードウェア識別子を指定します。
ms.assetid: b870e8fb-21b4-439b-b858-c45bf9be2ec1
keywords:
- INF モデルセクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF Models Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a78f7a024ed52f03866d794d746efe9af4578fb
ms.sourcegitcommit: 631cd4a65d49a071596920d764eeb660ad25ce7f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2019
ms.locfileid: "74953966"
---
# <a name="inf-models-section"></a>INF Models セクション


[製造元別*モデル*] セクションでは、少なくとも1つのデバイスを識別し、そのデバイスの INF ファイルの*ddinstall*セクションを参照して、そのデバイスの一意のモデルセクション[ハードウェア識別子 (ID)](hardware-ids.md)を指定します。

[製造元別*モデル*] セクションのエントリでは、初期ハードウェア ID で指定されたデバイスと互換性があり、同じドライバーによって制御されるモデルに対して、1つまたは複数の追加のデバイス id を指定することもできます。

```ini
[models-section-name] |
[models-section-name.TargetOSVersion]  (Windows XP and later versions of Windows)

device-description=install-section-name,[hw-id][,compatible-id...]
[device-description=install-section-name,[hw-id][,compatible-id]...] ...
```

> [!NOTE]
> Inf では、[モデル] セクションの各エントリに少なくとも1つのデバイス ID を指定する必要があります。  ハードウェア ID または互換性のある ID のいずれかになります。

## <a name="entries"></a>エントリ


<a href="" id="device-description"></a>*デバイス-説明*  
インストールするデバイスを識別します。これは、表示文字の一意の組み合わせ、または[**INF 文字列セクション**](inf-strings-section.md)で定義されている **%** <em>strkey</em> **%** トークンとして表現されます。 デバイスの説明の最大文字数は LINE_LEN。

<a href="" id="install-section-name"></a>*install-section-name*  
デバイス (および互換性のあるデバイスのモデル (存在する場合)) に使用する INF インストールセクションの非装飾名を指定します。 詳細については、「 [**INF *ddinstall* 」セクション**](inf-ddinstall-section.md)を参照してください。

<a href="" id="hw-id"></a>*hw id*  
デバイスを識別するベンダー定義の[ハードウェア ID](hardware-ids.md)文字列を指定します。この文字列は、PnP マネージャーがこのデバイスの INF ファイルの一致を検索するために使用します。 このようなハードウェア ID には、次のいずれかの形式があります。

<a href="" id="enumerator-enumerator-specific-device-id"></a>*列挙子\\列挙子-デバイス id*  
は、1つの列挙子によって PnP マネージャーに報告される個々の PnP デバイスの一般的な形式です。 たとえば、`USB\VID_045E&PID_00B` は、USB バス上の Microsoft HID キーボードデバイスを識別します。 列挙子に応じて、このような仕様には、デバイスのハードウェアリビジョン番号を含めることもできます (たとえば、`PCI\VEN_1011&DEV_002&SUBSYS_00000000&REV_02`)。

<a href="" id="-enumerator-specific-device-id"></a> *\*列挙子-デバイス id*  
デバイスが複数の列挙子によってサポートされていることをアスタリスク (\*) で示します。 たとえば、`*PNP0F01` は Microsoft のシリアルマウスを識別します。これには、`SERENUM\PNP0F01`と互換性のある id が指定されています。

<a href="" id="device-class-specific-id"></a>*デバイスクラス固有 ID*  
は、バスのハードウェア仕様で説明されている i/o バス固有の形式で、その種類の i/o バス上のすべての周辺機器のハードウェア Id を示します。

1つのデバイスに複数の*hw id*値を割り当てることができることに注意してください。 PnP マネージャーは、このような各*hw id*値を使用します。これらの値は通常、基になるバスによって子デバイスが列挙されるときに提供され、registry **Enum**分岐でそのような各デバイスのサブキーを作成します。 手動でインストールされたデバイスの場合、システムのセットアップコードは、それぞれの INF ファイルで指定されている*ハードウェア id*の値を使用して、このようなレジストリサブキーを作成します。

<a href="" id="compatible-id"></a>*互換性-id*  
互換性のあるデバイスを識別する、ベンダー定義の[互換性のある ID](compatible-ids.md)文字列を指定します。 [*モデル*] セクションのエントリには、任意の数の*互換性のある id*値を指定できます。各エントリは、次のコンマ ( **,** ) で区切られます。 このような互換性のあるすべてのデバイスまたはデバイスモデルは、初期の*hw id*で指定されたデバイスと同じドライバーによって制御されます。

<a name="remarks"></a>注釈
-------

各*モデル-セクション名*は、inf ファイルの[**inf 製造元セクション**](inf-manufacturer-section.md)に記載されている必要があります。 特定の製造元に対して INF ファイルをインストールするデバイス (およびドライバー) の数によっては、製造元ごとの*モデル*セクションに1つ以上のエントリが存在する場合があります。

各*インストールセクション名*は、inf ファイル内で一意である必要があります。また、「 [Inf ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」で説明されているセクション名を定義するための一般的な規則に従う必要があります。 「製造元別*モデル*」セクションで参照されている[***ddinstall***](inf-ddinstall-section.md)セクション名には、指定された*インストールセクション名*に拡張機能を追加することもできます。これにより、特定のデバイスの OS 固有またはプラットフォーム固有のインストールに対して追加の*ddinstall*セクションを定義できます。 クロスプラットフォームシステムファイルで拡張機能を使用する方法の詳細については、「 [INF ファイルの作成](overview-of-inf-files.md)」も参照してください。

指定された*hw id*または*互換性のある id*の値を[**INF controlflags セクション**](inf-controlflags-section.md)で指定して、手動インストール中にデバイスがエンドユーザーに表示されないようにすることもできます。 *Hw id*と*互換性のある id*の値の詳細については、「[デバイス id 文字列](device-identification-strings.md)」を参照してください。

INF ファイルを使用してインストールされたデバイスとドライバーごとに、デバイスインストーラーでは、[ [**inf の製造元] セクション**](inf-manufacturer-section.md)と [製造元別の*モデル*] セクションに記載されている情報を使用して、デバイスの説明、製造元の名前、デバイス ID (インストールが手動の場合)、および場合によってはレジストリ内の互換性リストの値のエントリ

*モデルセクション名*には、 *TargetOSVersion*装飾を含めることができます。 この装飾の詳細については、「 [**INF の製造元」セクション**](inf-manufacturer-section.md)、特に「解説」を参照してください。

**重要**  Windows SERVER 2003 SP1 以降では、inf ファイルは、関連する inf*モデル*セクション名と共に、 **ntia64**または**ntamd64**プラットフォーム拡張機能を使用して、[inf の**製造元**] セクションの [*名前*] エントリを修飾し、非 x86 ターゲットオペレーティングシステムのバージョンを指定する必要があります。 これらのプラットフォーム拡張機能は、x86 ベースのターゲットオペレーティングシステムのバージョンまたは非 PnP ドライバーの INF ファイル (x64 ベースのアーキテクチャ用のファイルシステムドライバーの INF ファイルなど) の INF ファイルには必要ありません。 *モデル*セクション内の各エントリは、"*ドライバーノード*" と呼ばれることがあります。

 

<a name="examples"></a>例
--------

この例では、一部のデバイス/モデルに対して[***Ddinstall***](inf-ddinstall-section.md)セクションを定義して、システムマウスクラスインストーラーの INF ファイルのいくつかの代表的なエントリを含む、製造元別*モデル*のセクションを示します。

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

[**Manufacturer**](inf-manufacturer-section.md)

[**Strings**](inf-strings-section.md)

 

 






