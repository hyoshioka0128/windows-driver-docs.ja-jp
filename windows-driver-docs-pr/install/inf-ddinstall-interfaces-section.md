---
title: INF DDInstall.Interfaces セクション
description: モデルごとの DDInstall. Interface セクションには、特定のデバイスまたはドライバーがサポートするデバイスインターフェイスの数に応じて、1つまたは複数の AddInterface ディレクティブを含めることができます。
ms.assetid: 16904119-00a4-45d7-a32e-24ba4c8a3416
keywords:
- INF DDInstall. インターフェイスセクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF DDInstall.Interfaces Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5a4e9600064587711bb24c7e8f030090a552cc9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837475"
---
# <a name="inf-ddinstallinterfaces-section"></a>INF DDInstall.Interfaces セクション


各モデルの<em>Ddinstall がインストール</em>**します。Interface**セクションには、特定のデバイスまたはドライバーがサポートするデバイスインターフェイスの数に応じて、1つまたは複数の[**addinterface**](inf-addinterface-directive.md)ディレクティブを含めることができます。

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

システムの定義済みのカーネルストリーミングインターフェイスなど、既存のデバイスインターフェイスをサポートするには、このセクションで適切な*InterfaceClassGUID*値を指定します。

新しいクラスのデバイスインターフェイスをエクスポートするコンポーネント (クラスドライバーなど) をインストールするには、INF にも[**Inf InterfaceInstall32 セクション**](inf-interfaceinstall32-section.md)が必要です。

デバイスインターフェイスの詳細については、「[デバイスインターフェイスクラス](device-interface-classes.md)」を参照してください。

## <a name="entries"></a>エントリ


<a href="" id="addinterface--interfaceclassguid------reference-string-----add-interface-section----flags-------"></a>**Addinterface = {** <em>InterfaceClassGUID</em> **}** \[ **、** \[*参照文字列*\] \[ **、** \[*追加インターフェイスセクション*\] \[ **、** \]\]\]フラグ...  
このディレクティブは、ドライバーが上位レベルのコンポーネントにエクスポートする、指定された*InterfaceClassGUID*値によって指定されるデバイスインターフェイスクラスのサポートをインストールします。 通常、inf ファイル内の他の場所で INF ライターによって定義された*インターフェイスセクション*も参照します。 このディレクティブを指定する方法の詳細については、「 [**INF AddInterface ディレクティブ**](inf-addinterface-directive.md)」を参照してください。

<a href="" id="include-filename-inf--filename2-inf----"></a>**Include =** <em>filename</em> **\[** **,** <em>filename2</em> **\].** ..  
この省略可能なエントリは、このデバイス/ドライバーでサポートされているインターフェイスクラスを登録するために必要なセクションを含む、追加のシステム提供の INF ファイルを1つ以上指定します。 このエントリが指定されている場合は、通常、**必要**なエントリです。

**インクルード**エントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a href="" id="needs-inf-section-name--inf-section-name----"></a>**必要な =** <em>inf-name</em>\[ **,** <em>inf-name</em>\]...  
この省略可能なエントリは、このデバイスのインストール中に処理する必要がある特定のセクションを指定します。 通常、このような名前付きセクションは、 <em>Ddinstall</em>**です。** **インクルード**エントリに一覧表示されている、システム提供の INF ファイル内のインターフェイスセクション。 ただし、このような<em>Ddinstall</em>内で参照される任意のセクションを指定でき**ます。** インクルードされている INF のインターフェイスセクション。

**必要**なエントリを入れ子にすることはできません。 **必要**なエントリとその使用に関する制限の詳細については、「[デバイスファイルのソースとターゲットの場所の指定](specifying-the-source-and-target-locations-for-device-files.md)」を参照してください。

<a name="remarks"></a>注釈
-------

*Ddinstall*セクション名は、INF ファイルの "製造元別*モデル*" セクションのデバイス/モデル固有のエントリで参照されている必要があります。 クロスプラットフォームの INF ファイルで、システムで定義された**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能を使用する方法については、「[複数のプラットフォーム用の INF ファイルの作成」と「オペレーティングシステム](creating-inf-files-for-multiple-platforms-and-operating-systems.md)。

指定した **{** <em>InterfaceClassGUID</em> **}** がまだインストールされていない場合、オペレーティングシステムのセットアップコードによって、そのデバイスインターフェイスクラスがシステムにインストールされます。 1つまたは複数の新しいデバイスインターフェイスクラスを INF ファイルでインストールする場合は、新しいクラスの GUID を識別する **\[InterfaceInstall32\]** セクションもあります。「」を参照してください。

GUID を作成する方法の詳細については、「[ドライバーでの guid の使用](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-guids-in-drivers)」を参照してください。 システム定義のインターフェイスクラス Guid については、カーネルストリームインターフェイスクラス GUID の*Ks*など、システムによって提供される適切なヘッダーを参照してください。

ドライバーが読み込まれるときに、INF の<em>ddinstall</em>に指定されている **{** <em>InterfaceClassGUID</em> **}** の値ごとに[**iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出す必要があり**ます。** 上位レベルのコンポーネントによって実行時に使用されるインターフェイスを有効にするために、ドライバーが基になるデバイスでサポートするインターフェイスセクション。 デバイスドライバーは、デバイスインターフェイスのサポートを INF に登録する代わりに、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出してから**Iosetdeviceinterfacestate**への最初の呼び出しを行うことができます。 通常、PnP 関数またはフィルタードライバーは、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンからこの呼び出しを行います。

<a name="examples"></a>例
--------

この例は、 <em>Ddinstall</em> **. nt を示しています。** システムが提供する WDM オーディオデバイス/ドライバーの inf ファイルのインターフェイスセクション。 [**Inf *ddinstall*セクション**](inf-ddinstall-section.md)と inf ddinstall の例として示されて[**います。サービスセクション**](inf-ddinstall-services-section.md)。

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

[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)

[**IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)

[***モジュール***](inf-models-section.md)

 

 






