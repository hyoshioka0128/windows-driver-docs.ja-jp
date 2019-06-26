---
title: プリンター ドライバーの INF ファイルで装飾を使用する方法
description: プリンター ドライバーの INF ファイルで装飾を使用する方法
ms.assetid: 772e2797-8019-4715-870c-b7cd2b8e65f2
keywords:
- 複数のプロセッサ アーキテクチャの WDK プリンター
- x86 ベースのドライバーのサンプルの WDK プリンター
- Itanium ベースのドライバーのサンプルの WDK プリンター
- 非装飾の INF WDK プリンター
- WDK の INF ファイルを印刷する装飾
- 装飾の INF WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bc627d388c65e3e785f2b4dc7bc3a36732eed25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378586"
---
# <a name="how-to-use-decorations-in-inf-files-for-printer-drivers"></a>プリンター ドライバーの INF ファイルで装飾を使用する方法


Windows Server 2003 SP1 以降で実行されるプリンター ドライバーまたは 64 ビット バージョンの Windows XP 以降を対象とする x64 では、アーキテクチャを装飾に含める必要があります[ **INF モデル セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)よう次の例です。 ただし、Windows Server 2003 SP1 の前に Windows のバージョンで追加のドライバーとドライバーをインストールする場合があります、ために、INF ファイル非装飾の INF モデル セクションが提供することする必要がありますも。 Itanium ベースのドライバーをインストールする文字装飾を使用することをお勧めします。

次の例では、1 つのプロセッサ アーキテクチャ用のドライバーをインストールするために使用する INF ファイルを書き込む方法を示します。

### <a name="x64-driver-sample"></a>x64 ドライバのサンプル

最初の例では、非装飾の INF モデル」セクションを使用して x64 をインストールする方法を示しています。 または、x86 または Windows XP または Windows Server 2003 を実行している Itanium ベースのコンピューターで Windows XP では、前に、Windows のバージョンのドライバーです。 2 番目のモデルの INF セクション NTamd64 装飾が x64 Windows Server 2003 SP1 以降を実行しているプロセッサのアーキテクチャのコンピューターにインストールするドライバー。

```cpp
[MANUFACTURER]
%Acme Corp.% = Acme, NTamd64
...

[Acme]
"Acme LaserWhiz 100 PS" = Acme100_x64.PPD, <hardware IDs and compatible IDs for this printer>

[Acme.NTamd64]
"Acme LaserWhiz 100 PS" = Acme100_x64.PPD, <hardware IDs and compatible IDs for this printer>
```

### <a name="itanium-based-driver-sample"></a>Itanium ベースのドライバーのサンプル

例を次に示します非装飾の INF を使用するモデルのセクションのバージョンの Windows XP では、前に Windows または x86、Itanium ベースのドライバーをインストールするマシンの方法を SP1 より前に、の Windows Server 2003 または Windows XP を実行します。 2 番目のモデルの INF セクション NTia64 装飾は、Itanium ベースのドライバーの Windows Server 2003 SP1 以降を実行しているプロセッサのアーキテクチャのコンピューターにインストールするとします。

```cpp
[MANUFACTURER]
%Acme Corp.% = Acme, NTia64
...

[Acme]
"Acme LaserWhiz 100 PS" = Acme100_ia64.PPD, <hardware IDs and compatible IDs for this printer>

[Acme.NTia64]
"Acme LaserWhiz 100 PS" = Acme100_ia64.PPD, <hardware IDs and compatible IDs for this printer>
```

### <a name="x86-driver-sample"></a>x86 ドライバーのサンプル

次の例では、モデルの INF セクションでは、装飾は必要ありません。 非装飾のセクションでは、x86 を参照すると見なされますので、プロセッサ アーキテクチャを指定する必要はありませんドライバー。 INF モデル NTx86 装飾では、セクションを追加する Windows Server 2003 SP1 の前に Windows のバージョンの非装飾の INF モデル セクションを含める必要がありますもことに注意してください。

```cpp
[MANUFACTURER]
%Acme Corp.% = Acme
...

[Acme]
"Acme LaserWhiz 100 PS" = Acme100_x86.PPD, <hardware IDs and compatible IDs for this printer>
```

### <a name="supporting-multiple-architectures-in-a-single-inf-file"></a>1 つの INF ファイルでの複数のアーキテクチャのサポート

このセクションでは、複数のプロセッサ アーキテクチャ用のプリンター ドライバーをインストールするために使用する INF ファイルを作成する方法を示します。

複数のアーキテクチャ用のドライバーをインストールするために使用する INF ファイルを作成するには、INF モデルのセクションでは、書き込みし、し、必要に応じて、そのコピーは、サポートされている各アーキテクチャに独自のモデルの INF セクションがありますようにします。 次の例に示すように、結果のモデルの INF セクションの各プロセッサ アーキテクチャごとに適切な装飾を追加します。

```cpp
[MANUFACTURER]
%Acme Corp% = Acme, NTamd64, NTia64
...

;; Used to install
;;    - a driver of any architecture type, on a machine running Windows 2000
;;    - a driver of any architecture type, on an x86 machine running Windows XP or Windows Server 2003
;;    - an x86 driver on a machine of any architecture type, running Windows Server 2003 with SP1
[Acme]
%Acme Model 1% = Acme100PS, <hardware IDs and compatible IDs for this printer>

;; Used to install
;;    - an x64 driver on a machine of any architecture type, running Windows Server 2003 with SP1
[Acme.NTamd64]
%Acme Model 1% = Acme100PS, <hardware IDs and compatible IDs for this printer>

;; Used to install
;;    - a driver of any architecture type, on an Itanium-based machine running Windows XP or Windows Server 2003
;;    - an Itanium-based driver on a machine of any architecture type, running Windows Server 2003 with SP1
[Acme.NTia64]
%Acme Model 1% = Acme100PS, <hardware IDs and compatible IDs for this printer>

;; DDInstall Section. 
;; This sample assumes that all three versions of the driver 
;; use the same DDInstall section.
[Acme100PS]
CopyFiles = MyDriverFile.dll, ...

[DestinationDirs]
DefaultDestDir=66000

[SourceDisksNames.x86]
1= %Location%,,,

[SourceDisksFiles.x86]
MyDriverFile.dll = 1,\i386
...

[SourceDisksNames.amd64]
1= %Location%,,,

[SourceDisksFiles.amd64]
MyDriverFile.dll = 1,\amd64
...

[SourceDisksNames.ia64]
1= %Location%,,,

[SourceDisksFiles.ia64]
MyDriverFile.dll = 1,\ia64
...

[Strings]
Acme Corp = "Acme Corporation"
Acme Model 1 = "Acme LaserWhiz 100 PS"
Location = "Acme CD ROM"
```

 

 




