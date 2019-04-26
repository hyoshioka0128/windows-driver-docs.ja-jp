---
title: INF ファイルの参照
description: INF ファイルの参照
ms.assetid: 4d9d5f28-b643-4369-8bf8-94703e8926d2
keywords:
- INF ファイル WDK デバイス インストールでは、構造体
- INF ファイルのセクションでは、WDK のデバイス インストール
- WDK の INF ファイルのセクションでは
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dfc3fb3a6eb63d47e5d829be12a0c3b1e73ee2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346826"
---
# <a name="looking-at-an-inf-file"></a>INF ファイルの参照





次の例では、任意の INF ファイルに配布する方法セクションでは、その一部は、参照の追加エントリ 0 個以上の行を含む各の INF ライター定義を表示する、システムが提供するクラスのインストーラーの INF ファイルから選択されたフラグメントセクション:

```cpp
[Version]
Signature="$Windows NT$"
Class=Mouse
ClassGUID={4D36E96F-E325-11CE-BFC1-08002BE10318}
Provider=%Provider% ; defined later in Strings section
DriverVer=09/28/1999,5.00.2136.1
 
[DestinationDirs]
DefaultDestDir=12 ; DIRID_DRIVERS
 
; ... [ControlFlags] section omitted here
 
[Manufacturer]
%StdMfg%    =StdMfg         ; (Standard types)
%MSMfg%     =MSMfg          ; Microsoft
; ... %otherMfg% entries omitted here
 
[StdMfg]  ; per-Manufacturer Models section 
; Std serial mouse
%*pnp0f0c.DeviceDesc%= Ser_Inst,*PNP0F0C,SERENUM\PNP0F0C,SERIAL_MOUSE
; Std InPort mouse
%*pnp0f0d.DeviceDesc%      = Inp_Inst,*PNP0F0D
     ; ... more StdMfg entries and following
     ; MSMfg and xxMfg Models sections omitted here
 
     ; per-Models DDInstall (Ser_Inst, Inp_Inst, etc.)
     ; sections also omitted here
 
[Strings] 
; where INF %strkey% tokens are defined as user-visible (and
; possibly as locale-specific) strings.
Provider = "Microsoft"
; ...
StdMfg   = "(Standard mouse types)"
MSMfg    = "Microsoft"
 
; ...
*pnp0f0c.DeviceDesc   = "Standard Serial Mouse"
*pnp0f0d.DeviceDesc   = "InPort Adapter Mouse"
; ... 
HID\Vid_045E&Pid_0009.DeviceDesc = "Microsoft USB Intellimouse"
; ... 
```

前の INF ファイル内のセクションでは、いくつかのシステム定義の名前はなどがある**バージョン**、 **DestinationDirs**、**製造元**、および**文字列**. 名前付きのようなセクションを一部**バージョン**、 **DestinationDirs**、および**文字列**だけの単純なエントリがあります。 前の例で示すように、INF ライター定義の追加のセクションを参照他のユーザー、**製造元**セクション。

マウス デバイス ドライバーのインストール以降のセクションでは関連の暗黙的な階層構造に注意してください、**製造元**前の例」セクション。 次の図は、INF ファイルでいくつかのセクションの階層を示します。

![inf ファイルのセクションのサンプルの階層を示す図](images/inf-sections.png)

INF ファイルの暗黙的な階層については、次に注意してください。

- 各**%** <em>xx</em>製造<strong>%</strong> 内のエントリ、**製造元**セクションごとに製造元の参照*モデル*INF ファイルで別の場所のセクション (StdMfg、MSMfg)。

  前の例では、エントリを使用して、%*strkey*% トークンです。

- 各*モデル*セクションがいくつかのエントリを指定します。 これらは、例では**%** <em>xxx</em>します。DeviceDesc<strong>%</strong>トークンです。

  これらの各**%** <em>xxx</em>します。DeviceDesc<strong>%</strong>トークンがいくつかのモデルごとに参照*DDInstall*各エントリで、その製造元の製品ラインのセクション (Ser_Inst と Inp_Inst)1 台のデバイスを識別する (\*PNP0F0C と\*PNP0F0D ためのここで示すように"DeviceDesc") または一連のデバイスの互換性のあるモデル。

- これらの各*DDInstall*-型*Xxx*_Inst セクションでは、さらに、追加された特定のシステム定義されている拡張子を持つことができますや、INF ライター定義の追加のセクションを参照するディレクティブを含めることができます。 たとえば、前の例のフラグメントとして表示される完全な INF ファイルでも、Ser_Inst があります<strong>します。サービス</strong>セクション、およびその Ser_Inst セクションが、 **CopyFiles**この INF ファイルの他の場所で Ser_CopyFiles セクションを参照するディレクティブ。

 

 





