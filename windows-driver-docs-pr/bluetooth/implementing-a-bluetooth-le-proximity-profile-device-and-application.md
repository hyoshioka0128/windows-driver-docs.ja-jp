---
title: Bluetooth LE 近接プロファイルの概要
description: 近接検出では、Bluetooth 低エネルギー (LE) の一般的な用途です。
ms.assetid: 4BF27CBE-C89A-48DC-8536-1A5111CDB0C4
ms.date: 07/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 355aaf293adae94bdbb2e0850c34a5857307261c
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608471"
---
# <a name="bluetooth-le-proximity-profile-overview"></a>Bluetooth LE 近接プロファイルの概要


近接検出では、Bluetooth 低エネルギー (LE) の一般的な用途です。 Windows 8 で導入された Bluetooth LE サポートで Windows 8.1 を展開します。 このセクションでは、Windows 8.1 と互換性がある UWP デバイス アプリの開発に使用できる近接プロファイルのデバイスの実装を作成するためのガイドラインを提供します。

このアプリを開発する前に Bluetooth LE 関数と Bluetooth LE 近接プロファイル仕様に慣れておく必要があります。

## <a name="span-idexampleservicedeclarationspanspan-idexampleservicedeclarationspanspan-idexampleservicedeclarationspanexample-service-declaration"></a><span id="Example_Service_Declaration"></span><span id="example_service_declaration"></span><span id="EXAMPLE_SERVICE_DECLARATION"></span>サービスの宣言の例


Bluetooth 低エネルギーは、Bluetooth の基本的なレートと同じ周波数領域を共有する新しい物理レイヤーを導入します。 低エネルギー プロファイルは、汎用の属性のプロファイル (または GATT) と呼ばれるものが編成されます。

GATT プロファイルは、ユース ケースやシナリオを定義する 1 つまたは複数のサービスを宣言します。 準拠しているサービスの実装を開発する必要がありますを整理する*特性*で定義されている確立されたスキーマに準拠しているように、 [Bluetooth Special Interest グループ (SIG) 開発者向けの web サイト](https://go.microsoft.com/fwlink/p/?linkid=320723).

この図はどのように*特性*一般的な GATT サービス内で構造化されます。

![gatt サービス宣言の例](images/bthleservicedeclaration.png)

近接通信プロファイルの例の詳細については[Bluetooth 近接プロファイル](bluetooth-proximity-profile.md)します。

 

 





