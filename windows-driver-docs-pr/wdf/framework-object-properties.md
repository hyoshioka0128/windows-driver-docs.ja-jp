---
title: Framework オブジェクトのプロパティ
description: Framework オブジェクトのプロパティ
ms.assetid: d95a7f51-fe22-4cd6-8c46-6d571f7d9169
keywords:
- framework オブジェクト WDK KMDF、プロパティ
- WDK KMDF のプロパティ
- get WDK KMDF メソッド
- WDK KMDF の set メソッド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcf8e9879929a8f08325ce6dbaa688c3c9920fd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551210"
---
# <a name="framework-object-properties"></a>Framework オブジェクトのプロパティ





ほとんどのフレームワーク オブジェクトには、プロパティのセットが含まれます。 プロパティは、ドライバーを使用できる情報を表します。 ドライバーの観点からいくつかのプロパティは読み取り専用と読み取り/書き込みをいくつか。

"Get"を定義するために、フレームワーク、読み取り可能な各プロパティの[メソッド](framework-object-methods.md)ドライバーは、プロパティの値を取得する呼び出すことができます。 各"get"メソッドでは、プロパティの現在の値を返します。

書き込み可能の各プロパティは、フレームワークは、ドライバーを呼び出すことができるプロパティの値を変更する「設定」のメソッドを定義します。 ドライバーは、"set"メソッドへの入力パラメーターとして、プロパティの新しい値を提供します。

たとえば、フレームワークのデバイス オブジェクトは 2 つのメソッドを定義します[ **WdfDeviceGetDeviceState** ](https://msdn.microsoft.com/library/windows/hardware/ff545994)と[ **WdfDeviceSetDeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff546884)、。プラグ アンド プレイ (PnP) の状態のドライバーは、デバイスの設定を取得または呼び出すことができます。

 

 





