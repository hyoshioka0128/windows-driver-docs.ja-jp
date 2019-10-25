---
title: フレームワーク オブジェクトのプロパティ
description: フレームワーク オブジェクトのプロパティ
ms.assetid: d95a7f51-fe22-4cd6-8c46-6d571f7d9169
keywords:
- フレームワークオブジェクト WDK KMDF、プロパティ
- WDK KMDF プロパティ
- get メソッド WDK KMDF
- set メソッド WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29e2bfe3c28fbb987e00ad4e0c2c8bbc7045c921
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845138"
---
# <a name="framework-object-properties"></a>フレームワーク オブジェクトのプロパティ





ほとんどのフレームワークオブジェクトには、一連のプロパティが含まれています。 プロパティは、ドライバーで使用できる情報を表します。 ドライバーの観点から見ると、一部のプロパティは読み取り専用であり、一部のプロパティは読み取り/書き込み可能です。

このフレームワークは、読み取り可能な各プロパティに対して、ドライバーがプロパティの値を取得するために呼び出すことができる "get"[メソッド](framework-object-methods.md)を定義します。 各 "get" メソッドは、プロパティの現在の値を返します。

フレームワークは、書き込み可能な各プロパティに対して、ドライバーがプロパティの値を変更するために呼び出すことができる "set" メソッドを定義します。 ドライバーは、プロパティの新しい値を入力パラメーターとして "set" メソッドに渡します。

たとえば、framework device オブジェクトでは、 [**Wdfdevicegetdevicestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdevicestate)と[**Wdfdevicegetdevicestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdevicestate)という2つのメソッドを定義しています。このメソッドを呼び出すと、デバイスのプラグアンドプレイ (PnP) 状態を取得または設定できます。

 

 





