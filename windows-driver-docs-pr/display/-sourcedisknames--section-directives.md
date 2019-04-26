---
title: '[SourceDiskNames] セクション ディレクティブ'
description: Windows Vista 以降、インボックス Inf は [SourceDisksXxx] ディレクティブを使用します。
ms.assetid: 0AC01548-3E53-41ED-9C7E-E33FC2DD14FD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3058ea992a1f6c4809369d30783ab7e69e385acf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346294"
---
# <a name="sourcedisknames-section-directives"></a>\[SourceDiskNames\]セクション ディレクティブ


Windows Vista 以降、インボックス Inf の使用、 *\[SourceDisksXxx\]* ディレクティブ。 ただし、これらのセクションの値は、何が通常された上記の独立系ハードウェア ベンダー (IHV) 実稼働のドライバー パッケージ内から変更されました。

## <a name="span-idsourcedisksnamesandsourcedisksfilessectiondirectivesspanspan-idsourcedisksnamesandsourcedisksfilessectiondirectivesspanspan-idsourcedisksnamesandsourcedisksfilessectiondirectivesspansourcedisksnames-and-sourcedisksfiles-section-directives"></a><span id="_SourceDisksNames__and__SourceDisksFiles__section_directives"></span><span id="_sourcedisksnames__and__sourcedisksfiles__section_directives"></span><span id="_SOURCEDISKSNAMES__AND__SOURCEDISKSFILES__SECTION_DIRECTIVES"></span>*\[SourceDisksNames\]* と*\[SourceDisksFiles\]* セクション ディレクティブ


たとえば、IHV 運用ドライバー。

``` syntax
For example, IHV production drivers:
[SourceDisksNames]
1 = %DiskID1%

[SourceDisksFiles]
r200.sys    = 1
r200umd.dll = 1
```

これは、Windows の受信トレイ INF 要件です。

``` syntax
[SourceDisksNames]
3426=windows cd

[SourceDisksFiles]
IHVKDM.sys      = 3426
IHVUMD.dll      = 3426
IHVVID.dll      = 3426
```

## <a name="span-idsignatureattributessectiondirectivesspanspan-idsignatureattributessectiondirectivesspanspan-idsignatureattributessectiondirectivesspansignatureattributes-section-directives"></a><span id="_SignatureAttributes__section_directives"></span><span id="_signatureattributes__section_directives"></span><span id="_SIGNATUREATTRIBUTES__SECTION_DIRECTIVES"></span>*\[SignatureAttributes\]* セクション ディレクティブ


受信トレイの Inf を使用して Windows vista 以降、 *\[SignatureAttributes\]* ディレクティブ。

ミニポート (.sys) ファイルを参照する必要はありません。

次に、例を示します。

``` syntax
[SignatureAttributes]
IHVUMD1.dll=SignatureAttributes.PETrust
IHVUMD2.dll=SignatureAttributes.PETrust

[SignatureAttributes.PETrust]
PETrust=true
```

 

 





