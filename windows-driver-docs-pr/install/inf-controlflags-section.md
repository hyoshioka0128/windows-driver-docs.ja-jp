---
title: INF ControlFlags セクション
description: ControlFlags セクションは、インストール中に Windows が特定の固有のアクションを実行する必要があるデバイスを識別します。
ms.assetid: 529060b6-ee4b-49a8-b723-5eda47e9f561
keywords:
- INF ControlFlags セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF ControlFlags Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce575b5a5c70ec084843ebb322fedec7e92e08c5
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038007"
---
# <a name="inf-controlflags-section"></a>INF ControlFlags セクション


**注**  ユニバーサルまたはモバイルのドライバーパッケージを作成している場合は、このセクションは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Controlflags**セクションは、インストール中に Windows が特定の固有のアクションを実行する必要があるデバイスを識別します。

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


<a href="" id="device-identification-string"></a>*デバイス id-文字列*  
製造元別の[**INF モデルセクション**](inf-models-section.md)で指定された[ハードウェア id](hardware-ids.md)または互換性のある[id](compatible-ids.md)を識別します。 各文字列は、次のコンマ (,) で区切る必要があります。

<a href="" id="excludefromselect"></a>**ExcludeFromSelect**  
すべてを削除します (\* が指定されている場合)。特定のユーザーインターフェイスから指定されたデバイスの一覧が表示される場合は、ユーザーが特定のデバイスを選択してインストールすることが想定されます。

Windows 2000 以降のバージョンの Windows では、新しいハードウェアの検出ウィザードとハードウェアの更新ウィザードによって、指定されたデバイスが表示されます。

OS と互換性のないデバイスまたはプラットフォームに互換性のないデバイスのセットをこのディスプレイから除外するには、1つまたは複数の**ExcludeFromSelect**エントリで、次のような大文字と小文字を区別しない拡張機能を追加します。

<a href="" id="-nt"></a> **. nt**  
Windows 2000 以降のバージョンの Windows を実行しているコンピューターでは、これらのデバイスを表示しません。

<a href="" id="-ntx86-"></a> **. ntx86**   
Windows 2000 以降のバージョンの Windows を実行している x86 ベースのコンピューターでは、これらのデバイスを表示しません。

<a href="" id="-ntia64--"></a> **. ntia64**   
Windows XP 以降のバージョンの Windows を実行している Itanium ベースのコンピューターでは、これらのデバイスを表示しません。

<a href="" id="-ntamd64"></a> **.ntamd64**  
Windows XP 以降のバージョンの Windows を実行している x64 ベースのコンピューターでは、これらのデバイスを表示しません。

<a href="" id="-ntarm"></a> **。 ntarm**  
Windows XP 以降のバージョンの Windows を実行している ARM ベースのコンピューターでは、これらのデバイスを表示しません。

<a href="" id="-ntarm64"></a> **.ntarm64**  
Windows XP 以降のバージョンの Windows を実行している ARM64 ベースのコンピューターでは、これらのデバイスを表示しません。



システム定義の**nt**、 **ntx86**、. **ntia64**、. **ntamd64**、. **ntarm**、および**ntarm64**の各拡張機能の使用方法の詳細については、「[複数のプラットフォームおよびオペレーティングシステム用の INF ファイルの作成](creating-inf-files-for-multiple-platforms-and-operating-systems.md)」を参照してください。

<a href="" id="copyfilesonly"></a>**CopyFilesOnly**  
では、デバイスハードウェアにアクセスできないか、または使用できないため、指定したデバイスに対して INF 指定のファイルのみがインストールされます。

このエントリはほとんど使用されません。 ただし、現在使用されている特定のスロットにカードが後で装着されるデバイスのドライバーをプレインストールするために使用できます。 たとえば、INF によって指定されたファイルをターゲットに転送するために、特定のスロットに現在装着されているデバイスが必要な場合は、INF にこのエントリが含まれます。

<a href="" id="interactiveinstall"></a>**InteractiveInstall**  
指定されたデバイスの一覧をユーザーのコンテキストに強制的にインストールします。 各行には、1つまたは複数のハードウェア Id または互換性のある Id を指定できます。また、1つまたは複数の行を指定できます。

このエントリは省略可能です。 デバイスをインストールするには、このエントリを省略し、可能であれば、信頼されたシステムスレッドのコンテキストでデバイスをインストールできるようにすることをお勧めします。 ただし、デバイスのインストール時にデバイスにユーザーがログインする必要がある場合は、デバイスの INF にこのエントリを含めます。

<a href="" id="requestadditionalsoftware"></a>**RequestAdditionalSoftware**  
すべて ( **\*** が指定されている場合)、または指定されたデバイスの一覧に、デバイスの[ドライバーパッケージ](driver-packages.md)を通じてインストールされたソフトウェアよりも追加のソフトウェアが必要な場合があることを指定します。 たとえば、 **Requestadditionalsoftware**エントリを使用すると、ドライバーパッケージに含まれていなかった新しいデバイスまたは更新されたソフトウェアをインストールできます。

**メモ** **\*** が指定されていない場合は、 **requestadditionalsoftware**エントリによって指定された各デバイスを、 [**INF モデルセクション**](inf-models-section.md)内で定義する必要があります。

 

このエントリはオプションであり、windows 7 以降のバージョンの Windows オペレーティングシステムでサポートされています。

Windows がデバイスの[ドライバーパッケージ](driver-packages.md)をインストールした後、プラグアンドプレイ (PnP) マネージャーは、 **requestadditionalsoftware**エントリが INF ファイル内で指定されている場合、次の手順を実行します。

1.  PnP マネージャーは、 **Requestaddtionalsoftware**の種類を使用して、問題レポートとソリューション (pr) エラー報告を生成します。 このレポートには、デバイスの特定のハードウェア ID と、コンピューターのシステムアーキテクチャに関する情報が表示されます。
2.  デバイス固有のソフトウェアに対して独立系ハードウェアベンダー (IHV) によって提供されるソリューションがある場合、ソリューションはコンピューターにダウンロードされます。

    **ただし**、ソリューションをダウンロードしてもソフトウェア自体はインストールされません  。

     

3.  デバイス固有のソフトウェアがコンピューターにインストールされていない場合、PnP マネージャーはそのソリューションをユーザーに提示し、ソフトウェアをダウンロードするためのリンクを提供します。 ユーザーは、ソリューションに記載されている手順に従って、このソフトウェアをダウンロードしてインストールすることを選択できます。

<a name="remarks"></a>注釈
-------

通常、 **Controlflags**セクションには、[製造元別の[**INF モデル] セクション**](inf-models-section.md)に一覧表示されているデバイスを識別する1つ以上の**ExcludeFromSelect**エントリがありますが、手動でインストールするときに、エンドユーザーにオプションとして表示されることはありません。

デバイスの[ハードウェア id](hardware-ids.md)または[互換性のある id](compatible-ids.md)を**ExcludeFromSelect**エントリに一覧表示すると、エンドユーザーに表示される表示から削除されます。 **ExcludeFromSelect**値にアスタリスク (\*) を指定すると、このユーザーに表示される一覧から、INF ファイルで定義されているすべてのデバイスとモデルが削除されます。

INF ライターは、次の状況でのみ、 **Interactiveinstall**ディレクティブを使用しないようにする必要があります。

-   ハードウェア Id が破損しているか、正しく定義されていないデバイスのドライバーをインストールする。 たとえば、2つ以上の異なるデバイスが同じハードウェア ID を共有している場合などです。 このケースはプラグアンドプレイ標準によって厳密には禁止されていますが、ハードウェアでこのエラーが発生したハードウェアベンダーもあります。
-   独自のドライバーを必要とするデバイスのドライバーをインストールする場合、または、オペレーティングシステムに用意されているジェネリッククラスドライバーまたはその他のドライバーを使用できない。 **Interactiveinstall**エントリは、互換性のある ID 一致の確認をユーザーに要求するようにデバイスマネージャーに強制します。

**注**  今後、WHQL では、INF ファイルに**interactiveinstall**エントリが含まれるデバイスに Windows ロゴが付与されない場合があります。

 

PnP デバイスを排他的にインストールする INF ファイルでは、各*Setupclassguid*レジストリキーの**NoInstallClass** value エントリを**TRUE**に設定しない限り、 **controlflags**セクションを持つことができます。 これらのレジストリキーの詳細については、「 [**INF ClassInstall32」セクション**](inf-classinstall32-section.md)を参照してください。

<a name="examples"></a>例
--------

システムのマウスクラスインストーラー INF の**Controlflags**セクションのこの例では、x86 プラットフォームにインストールできないデバイスやモデルの表示が抑制されています。

```ini
[ControlFlags]
; Exclude all bus mice and InPort mice for x86 platforms
ExcludeFromSelect.ntx86=*PNP0F0D,*PNP0F11,*PNP0F00,*PNP0F02,*PNP0F15
; Hide this entry always
ExcludeFromSelect=UNKNOWN_MOUSE
```

次の INF ファイルフラグメントでは、2つのデバイスが示されています。1つは完全な PnP 対応であり、インストール時にユーザーの操作は必要ありません。また、独自のドライバーを必要とし、他のドライバーを使用することはできません。 2番目のデバイスに**Interactiveinstall**を指定すると、Windows はこのデバイスをユーザーのコンテキスト (管理者権限を持つユーザー) にインストールするように強制されます。 これには、必要に応じて、ドライバーファイルの場所 (INF ファイル、ドライバーファイルなど) の入力をユーザーに求めることが含まれます。

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

[**Manufacturer**](inf-manufacturer-section.md)

[***モジュール***](inf-models-section.md)

 

 






