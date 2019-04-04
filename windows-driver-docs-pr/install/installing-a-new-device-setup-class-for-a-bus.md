---
title: バスの新しいデバイス セットアップ クラスをインストールします。
description: バスの新しいデバイス セットアップ クラスをインストールします。
ms.assetid: a94899b6-02e0-4181-bb14-5552806a8c9e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 663fb8f1155aaa98c567d3d98673192d1927aee9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557851"
---
# <a name="installing-a-new-device-setup-class-for-a-bus"></a>バスの新しいデバイス セットアップ クラスをインストールします。


新しいバスは、その機能は既存に属しているデバイスによって提供される機能と大幅に異なるデバイスをサポートしている場合[デバイス セットアップ クラス](device-setup-classes.md)バスの新しいデバイス セットアップ クラスをインストールする必要があります。 新しいデバイス セットアップ クラスをインストールするかどうかを判断するのに役立つ詳細については、[新しいデバイス セットアップ クラスを作成する](creating-a-new-device-setup-class.md)を参照してください。

バスの新しいデバイス セットアップ クラスをインストールする関連するディレクティブを設定、 [ **INF バージョン セクション**](inf-version-section.md)、含める、 [ **INF ClassInstall32 セクション**](inf-classinstall32-section.md)、INF Class32 セクションで参照されている、ために必要な追加のセクションが含まれます。

次の注釈付きの例は、インストールに含める必要がある基本的な INF ファイルのエントリを示しています、[デバイス セットアップ クラス](device-setup-classes.md)します。 デバイス セットアップ クラスの構成設定については、[ **INF ClassInstall32 セクション**](inf-classinstall32-section.md)を参照してください。

```cpp
[Version]
signature="$CHICAGO$"
; Specify a unique class name that identifies the manufacturer and the bus type
Class=%AbcSuperBus%

; Specify a unique GUID that identifies the device setup class
ClassGUID={17ed6609-9bc8-44ca-8548-abb79b13781b}

; Identify the provider of the INF file
Provider=%AbcCorp%

; Specify the version of the device driver
DriverVer=01/01/2007,1.0.0.0 

[ClassInstall32]
; Reference an AddReg directive that specifies class properties
Addreg=AbcSuperBusClassReg 

[AbcSuperBusClassReg]
; Specify the properties of the device setup class
HKR,,,,%AbcSuperBus%
HKR,,Icon,,-19
HKR,,NoInstallClass,,1
. . .
. . .
[Strings] 
AbcCorp="Abc Corporation"
AbcSuperBus="Abc Corporation Super Bus Controller"
```

 

 





