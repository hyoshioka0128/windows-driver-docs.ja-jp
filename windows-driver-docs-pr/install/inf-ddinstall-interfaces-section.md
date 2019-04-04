---
title: INF DDInstall.Interfaces セクション
description: -モデル DDInstall.Interfaces セクションには、特定のデバイス/ドライバーがサポートしているデバイス インターフェイスの数に応じて 1 つまたは複数の AddInterface ディレクティブことができます。
ms.assetid: 16904119-00a4-45d7-a32e-24ba4c8a3416
keywords:
- INF DDInstall.Interfaces セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.Interfaces Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfdcd6e7f8b96e80bad364a7b5f18cd199cf2bb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532115"
---
# <a name="inf-ddinstallinterfaces-section"></a>INF DDInstall.Interfaces セクション


各ごとのモデル<em>DDInstall</em>**します。インターフェイス**セクションは、1 つ以上を持つことができます[ **AddInterface** ](inf-addinterface-directive.md)ディレクティブでは、特定のデバイス/ドライバーがサポートしているデバイス インターフェイスの数によって異なります。

```ini
[install-section-name.Interfaces] |
[install-section-name.nt.Interfaces] | 
[install-section-name.ntx86.Interfaces] |
[install-section-name.ntarm.Interfaces] | (Windows 8 and later versions of Windows)
[install-section-name.ntarm64.Interfaces] | (Windows 10 version 1709 and later versions of Windows)
[install-section-name.ntia64.Interfaces] |  (Windows XP and later versions of Windows)
[install-section-name.ntamd64.Interfaces]  (Windows XP and later versions of Windows)
 
AddInterface={InterfaceClassGUID} [, [reference string] [,[add-interface-section] [,flags]]] ...
[Include=filename.inf[,filename2.inf]...]
[Needs=inf-section-name[,inf-section-name]...] 
```

既存のデバイスをサポートするなど、システムの定義済みカーネル ストリーミング インターフェイスのいずれかのインターフェイスに、適切な指定*InterfaceClassGUID*このセクションの値。

デバイス インターフェイスの新しいクラスをエクスポートするクラス ドライバーなど、コンポーネントをインストールする、INF が必要もあります、 [ **INF InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)します。

デバイス インターフェイスの詳細については、[デバイス インターフェイス クラス](device-interface-classes.md)を参照してください。

## <a name="entries"></a>エントリ


<a href="" id="addinterface--interfaceclassguid------reference-string-----add-interface-section----flags-------"></a>**AddInterface = {**<em>InterfaceClassGUID</em>**}** \[ **、** \[*文字列参照*\] \[ **、**\[*追加インターフェイス セクション*\] \[ **、** <em>フラグ</em>\] \] \] .  
このディレクティブの指定で指定された、デバイスのインターフェイス クラスのサポートをインストールする*InterfaceClassGUID*上位コンポーネントにドライバーをエクスポートする値。 通常も参照して、INF-ライター定義*追加インターフェイス セクション*INF ファイルで別の場所。 このディレクティブを指定する方法の詳細については、[ **INF AddInterface ディレクティブ**](inf-addinterface-directive.md)を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**含める =**<em>filename</em>**.inf**\[**、**<em>filename2</em>**.inf**\]...  
この省略可能なエントリでは、1 つまたは複数追加システムが指定した INF ファイルをこのデバイス/ドライバーでサポートされているインターフェイス クラスを登録するために必要なセクションが含まれているを指定します。 通常、このエントリが指定されている場合は、**必要がある**エントリ。

詳細については、 **Include**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =**<em>inf セクション名</em>\[**、**<em>inf セクション名</em>\].  
この省略可能なエントリでは、このデバイスのインストール中に処理する必要がある特定のセクションを指定します。 通常、このような名前付きセクションは、 <em>DDInstall</em>**します。インターフェイス**セクションに記載されているシステム指定の INF ファイル内で、 **Include**エントリ。 ただし、このような内で参照されている任意のセクションがあります、 <em>DDInstall</em>**します。インターフェイス**の含まれる INF セクション。

**必要がある**エントリを入れ子にすることはできません。 詳細については、**必要がある**エントリと、その使用に関する制限事項を参照してください。[デバイス ファイルのソースとターゲットの場所を指定する](specifying-the-source-and-target-locations-for-device-files.md)します。

<a name="remarks"></a>注釈
-------

*DDInstall*セクション名 - 製造元でデバイス/モデルに固有のエントリを参照する必要があります*モデル*INF ファイルのセクション。 システム定義を使用する方法については **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64**クロスプラット フォーム対応の INF ファイル、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

指定した場合 **{**<em>InterfaceClassGUID</em>**}** がインストールされていない既に、オペレーティング システムのセットアップ コードがシステムでそのデバイスのインターフェイス クラスをインストールします。 INF ファイルでは、1 つまたは複数の新しいデバイス インターフェイス クラスをインストールする場合、 **\[InterfaceInstall32\]** セクションの新しいクラスの GUID を特定する.

GUID を作成する方法の詳細については、[ドライバーを使用して Guid](https://msdn.microsoft.com/library/windows/hardware/ff565392)を参照してください。 システム定義のインターフェイス クラスの Guid など、システム提供の適切なヘッダーを参照してください*Ks.h*カーネル ストリーミング インターフェイスをクラスの GUID。

ドライバーが読み込まれるときに呼び出す必要があります[ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)ごとに 1 回 **{**<em>InterfaceClassGUID</em>**}** INF ので指定された値<em>DDInstall</em>**します。インターフェイス**より高いレベルのコンポーネントによって実行時用のインターフェイスを有効にする、基になるデバイスのドライバーをサポートしているセクション。 デバイス ドライバーを呼び出すことができます、INF デバイス インターフェイスのサポートを登録するではなく[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)その最初の呼び出しを行う前に**IoSetDeviceInterfaceState**. PnP 関数またはフィルター ドライバーからのこの呼び出しは、通常は、その[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。

<a name="examples"></a>例
--------

この例では、 <em>DDInstall</em>**.nt します。インターフェイス**システム提供されている WDM オーディオ デバイス/ドライバーの例として示す INF ファイルのセクション、 [ **INF *DDInstall*セクション**](inf-ddinstall-section.md)および[ **INF *DDInstall*します。サービス セクション**](inf-ddinstall-services-section.md)します。

```ini
;
; following AddInterface= are all single lines (without 
; backslash line continuators) in the system-supplied INF file
;
[WDMPNPB003_Device.NT.Interfaces]
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave%,\
  WDM_SB16.Interface.Wave
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Topology%,\
  WDM_SB16.Interface.Topology
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_UART%,\
  WDM_SB16.Interface.UART
AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_FMSynth%,\
  WDM_SB16.Interface.FMSynth
; ...

[Strings] ; only immediately preceding %strkey% tokens shown here
%KSCATEGORY_AUDIO% = "{6994ad04-93ef-11d0-a3cc-00a0c9223196}"
KSNAME_Wave = "Wave"
KSNAME_UART = "UART"
KSNAME_FMSynth = "FMSynth" 
KSNAME_Topology = "Topology"
; ...
```

## <a name="see-also"></a>関連項目


[**AddInterface**](inf-addinterface-directive.md)

[***DDInstall***](inf-ddinstall-section.md)

[**InterfaceInstall32**](inf-interfaceinstall32-section.md)

[**IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)

[**IoSetDeviceInterfaceState**](https://msdn.microsoft.com/library/windows/hardware/ff549700)

[***モデル***](inf-models-section.md)

 

 






