---
ms.assetid: 9f14c40b-0d6a-45d0-9c8b-6c5603fee3c6
title: API レイヤー化
description: Windows ドライバーを使うと、組み込みシステムからタブレットや PC まで、複数の種類のデバイスで動作する 1 つのドライバーを作成できます。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: be6989dd366fc443bab6a487c0cbefb849987b12
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270479"
---
# <a name="api-layering"></a>API レイヤー化

## <a name="overview"></a>概要

API レイヤー化では、Windows 10 の UWP ベース エディションに含まれている API および DDI、または選別された一連の Win32 API の API および DDI のみを Windows ドライバー パッケージのバイナリが呼び出す必要があります。 API レイヤー化は、DCHU 設計原則に含まれていた "U" 要件の延長です。

どのプラットフォームが API でサポートされているのかを確かめるには、API のドキュメント ページにアクセスし、要件セクションの**ターゲット プラットフォーム** エントリを確認してください。  Windows ドライバーでは、**ターゲット プラットフォーム**が `Universal` (機能のサブセットがすべての Windows 製品で利用できることを意味します) としてリストされている API または DDI のみを使用する必要があります。

## <a name="validating-api-layering"></a>API レイヤー化の検証  

[ApiValidator](https://docs.microsoft.com/windows-hardware/test/hlk/testref/df4a9671-c2aa-4c81-b964-7247fb4799df) は、Windows ドライバーの API レイヤー化のコンプライアンスを検証するために使用される主なツールです。  ApiValidator は、Windows Driver Kit (WDK) の一部として同梱されています。  

ApiValidator を使用して、Windows ドライバーが API レイヤー化の要件を満たしていることを確認する方法の詳細については、「[Windows ドライバーの検証](validating-windows-drivers.md)」を参照してください。
