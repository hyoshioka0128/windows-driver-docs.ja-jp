---
title: INF ControlFlags セクション
description: ControlFlags セクションでは、デバイスの Windows は、インストール中に特定の一意のアクションを実行する必要がありますを識別します。
ms.assetid: 529060b6-ee4b-49a8-b723-5eda47e9f561
keywords:
- INF ControlFlags セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ControlFlags Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f52af6a0d8677d494ec80d865041c326ba3a6f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530694"
---
# <a name="inf-controlflags-section"></a>INF ControlFlags セクション


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このセクションが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

A **ControlFlags**セクションは、対象の Windows は、インストール中に特定の一意のアクションを実行する必要がありますデバイスを識別します。

```ini
[ControlFlags]

ExcludeFromSelect=* | 
ExcludeFromSelect=device-identification-string[,device-identification-string] ...] | 
[ExcludeFromSelect.nt=device-identification-string[,device-identification-string] ...] | 
[ExcludeFromSelect.ntx86=device-identification-string[,device-identification-string] ...] | 
[ExcludeFromSelect.ntia64=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)
[ExcludeFromSelect.ntamd64=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)
[ExcludeFromSelect.ntarm=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)
[ExcludeFromSelect.ntarm64=device-identification-string[,device-identification-string] ...]  |  (Windows XP and later versions of Windows)

[CopyFilesOnly=device-identification-string[,device-identification-string] ...]
[InteractiveInstall=device-identification-string[,device-identification-string] ... ]
[RequestAdditionalSoftware=*] | 
[RequestAdditionalSoftware=device-identification-string[,device-identification-string] ...]  (Windows 7 and later versions of Windows)
```

## <a name="entries"></a>エントリ


<a href="" id="device-identification-string"></a>*デバイスの識別文字列*  
識別、[ハードウェア ID](hardware-ids.md)または[互換性 ID](compatible-ids.md)製造元ごとに指定されている[ **INF モデル セクション**](inf-models-section.md)します。 各文字列は、コンマ (,) で区切る必要があります。

<a href="" id="excludefromselect"></a>**ExcludeFromSelect**  
すべてを削除します (場合\*を指定) または指定したインストールの特定のデバイスを選択するユーザーを想定元となる特定のユーザー インターフェイス表示からデバイスの一覧。

Windows 2000 と Windows の以降のバージョンでは、指定したデバイスが新しいハードウェアの検出ウィザードとハードウェアの更新ウィザードで表示されます。

この表示、1 つまたは複数から一連の OS の互換性がないかプラットフォーム互換性のないデバイスを除外する**ExcludeFromSelect**エントリは追加された次大文字の拡張機能であることができます。

<a href="" id="-nt"></a>**.nt**  
Windows 2000 またはそれ以降のバージョンの Windows を実行しているコンピューターにこれらのデバイスは表示されません。

<a href="" id="-ntx86-"></a>**.ntx86**   
Windows 2000 またはそれ以降のバージョンの Windows を実行している x86 ベースのコンピューター上でこれらのデバイスは表示されません。

<a href="" id="-ntia64--"></a>**.ntia64**   
Windows XP または Windows の以降のバージョンを実行している Itanium ベースのコンピューター上でこれらのデバイスは表示されません。

<a href="" id="-ntamd64"></a>**.ntamd64**  
Windows XP または Windows の以降のバージョンを実行している x64 ベースのコンピューター上でこれらのデバイスは表示されません。

<a href="" id="-ntarm"></a>**.ntarm**  
Windows XP または Windows の以降のバージョンを実行している ARM ベースのコンピューター上でこれらのデバイスは表示されません。

<a href="" id="-ntarm64"></a>**.ntarm64**  
Windows XP または Windows の以降のバージョンを実行する ARM64 ベースのコンピューター上でこれらのデバイスは表示されません。



詳細については、システム定義を使用する方法についての **.nt**、 **.ntx86**、 **.ntia64**、 **.ntamd64**、 **.ntarm**、および **.ntarm64** 、拡張機能を参照してください[INF ファイルを複数のプラットフォームやオペレーティング システムを作成する](creating-inf-files-for-multiple-platforms-and-operating-systems.md)します。

<a href="" id="copyfilesonly"></a>**CopyFilesOnly**  
デバイスのハードウェア使用されていないアクセスまたは使用可能なため、特定のデバイスの INF で指定されたファイルのみをインストールします。

このエントリはほとんど使用されません。 ただしのカードが後に接続されている特定のスロットは現在使用中にデバイス ドライバーをプレインストールする使用することができます。 たとえば、現在特定のスロットに取り付けられているデバイスは、INF で指定されたファイルをターゲットに転送する必要がある場合、INF すると、このエントリがあります。

<a href="" id="interactiveinstall"></a>**InteractiveInstall**  
指定したユーザーのコンテキストでインストールするデバイスの一覧を強制します。 各行が 1 つまたは複数のハードウェア Id または互換性 Id を指定し、1 つまたは複数の行があります。

このエントリは省略可能です。 デバイスをインストールすることをお勧めは、このエントリを省略し、可能であれば、信頼済みのシステム スレッドのコンテキストでは、デバイスをインストールする Windows です。 ただし、デバイスにログインするユーザーを絶対に必要な場合、デバイスがインストールされている場合、デバイス INF でこのエントリが含まれます。

<a href="" id="requestadditionalsoftware"></a>**RequestAdditionalSoftware**  
指定しますすべて (場合**\\*** を指定) または指定したデバイスの一覧よりを通じてインストールされた追加のソフトウェアが必要とする可能性があります、[ドライバー パッケージ](driver-packages.md)デバイス。 たとえば、 **RequestAdditionalSoftware**エントリは、ドライバー パッケージに含まれていない新規または更新済みのデバイスに固有のソフトウェアをインストールするために使用できます。

**注**場合**\\*** が指定されていない、各デバイスがで指定された、 **RequestAdditionalSoftware**内でエントリを定義する必要があります、 [ **INFセクションをモデル化**](inf-models-section.md)します。

 

このエントリは、省略可能であり、Windows 7 およびそれ以降のバージョンの Windows オペレーティング システムでサポートされます。

Windows をインストールした後、[ドライバー パッケージ](driver-packages.md)場合、デバイスのプラグ アンド プレイ (PnP) マネージャーが、次の手順を実行、 **RequestAdditionalSoftware** INF ファイル内でエントリを指定します。

1.  PnP マネージャーでは、問題レポートとソリューション (PR) のエラー レポートを生成の型と**RequestAddtionalSoftware**します。 このレポートには、デバイスとコンピューターのシステム アーキテクチャの特定のハードウェア ID に関する情報が含まれています。
2.  デバイス固有のソフトウェアの独立系ハードウェア ベンダー (IHV) によって提供されるソリューションがある場合は、ソリューションがコンピューターにダウンロードされます。

    **注**  ソリューションのダウンロードでは、ソフトウェア自体はインストールされません。

     

3.  デバイス固有のソフトウェアがコンピューターにインストールされていない場合 PnP マネージャーは、ユーザーは、ソリューションと、ソフトウェアのダウンロード リンクを提供します。 ユーザーは、ダウンロードして、ソリューションに示される手順に従ってこのソフトウェアをインストールする選択できます。

<a name="remarks"></a>注釈
-------

通常、 **ControlFlags**セクションには 1 つまたは複数**ExcludeFromSelect**エントリの製造元に記載されているデバイスを識別する[ **INF モデル セクション**](inf-models-section.md)は表示されません、エンドユーザーにオプションとして手動のインストール中にします。

デバイスの一覧表示[ハードウェア ID](hardware-ids.md)または[互換性 ID](compatible-ids.md)で、 **ExcludeFromSelect**エントリは、エンドユーザーに示されている表示から削除します。 アスタリスクを指定する (\*) の**ExcludeFromSelect**値は、このユーザーに表示される一覧から、INF ファイルで定義されているすべてのデバイス/モデルを削除します。

INF ライターを使用する必要があります、 **InteractiveInstall**ディレクティブ控えめと、次の状況でのみ。

-   それ以外の場合正しく定義されていないハードウェア Id または破損しているデバイスのドライバーをインストールします。 たとえば、2 つ以上のさまざまなデバイスが同じハードウェア ID を共有場合 この場合は、標準のプラグ アンド プレイによって禁じられていますが、一部のハードウェア ベンダーがハードウェアでこのエラーを行った。
-   独自のドライバーを必要とし、どうしてもことはできません、ジェネリック クラス ドライバーまたは提供されている別のドライバー、オペレーティング システムで使用するデバイスのドライバーをインストールします。 **InteractiveInstall**エントリはデバイス マネージャーとが一致する互換性 ID の確認をユーザーに確認します。

**注**  今後、WHQL 付与されない INF ファイルに含めるデバイスの Windows ロゴ**InteractiveInstall**エントリ。

 

PnP デバイスを排他的にインストールする INF ファイルを持つことができます、 **ControlFlags**セクションが設定されていない限り、 **NoInstallClass** 、それぞれのエントリの値*SetupClassGUID*レジストリ キーを押して**TRUE**します。 これらのレジストリ キーの詳細については、次を参照してください。 [ **INF ClassInstall32 セクション**](inf-classinstall32-section.md)します。

<a name="examples"></a>例
--------

この例の**ControlFlags**システム マウス クラス インストーラー INF セクションは、x86 上でインストールできないデバイス/モデルの表示を抑制します。 プラットフォーム。

```ini
[ControlFlags]
; Exclude all bus mice and InPort mice for x86 platforms
ExcludeFromSelect.ntx86=*PNP0F0D,*PNP0F11,*PNP0F00,*PNP0F02,*PNP0F15
; Hide this entry always
ExcludeFromSelect=UNKNOWN_MOUSE
```

次の INF ファイル フラグメントは、2 つのデバイスを示しています。 完全 PnP 対応であり、中にインストールし、独自のドライバーを必要とし、他のドライバーを使用することはできません他のユーザーの介入は必要ありません。 指定する**InteractiveInstall** 2 番目のデバイスがこのデバイスをユーザーのコンテキスト (管理者権限を持つユーザー) にインストールする Windows を強制します。 これは、必要なドライバー ファイル (INF ファイル、ドライバー ファイル、およびなど) の場所をユーザーに確認が含まれます。

```ini
; ...
[Manufacturer]
%Mfg% = ModelsSection

[ModelsSection]
; Models section, with two entries
%Device1.DeviceDesc% = Device1.Install, \
    PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_01
%Device2.Device.Desc%= Device2.Install, \
    PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02

[ControlFlags]
InteractiveInstall = \
  PCI\VEN_1000&DEV_0001&SUBSYS_00000000&REV_02
; ...
```

## <a name="see-also"></a>関連項目


[**ClassInstall32**](inf-classinstall32-section.md)

[**製造元**](inf-manufacturer-section.md)

[***モデル***](inf-models-section.md)

 

 






