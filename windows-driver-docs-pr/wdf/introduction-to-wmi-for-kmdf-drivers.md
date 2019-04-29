---
title: KMDF ドライバー用の WMI の概要
description: KMDF ドライバー用の WMI の概要
ms.assetid: e919f6c9-a4c5-4972-91e7-f4fa609455fe
keywords:
- WMI の WDK KMDF
- フレームワーク ベースのドライバーの WMI の詳細について、WMI の WDK KMDF
- WDK KMDF のコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ab7d04fdef5c59b7682f3780f03f5ba339c28b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388612"
---
# <a name="introduction-to-wmi-for-kmdf-drivers"></a>KMDF ドライバー用の WMI の概要


\[KMDF にのみ適用されます。\]

カーネル モード ドライバー フレームワークに情報を提供するドライバーをサポートしている[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff548187) (WMI)。 このようなドライバーが呼び出されて*データ プロバイダーの WMI*データを提供するため、 *WMI クライアント*、WMI から情報を受信登録されているアプリケーションであります。

WMI データ プロバイダーのサポート*WMI データ ブロック*次の 1 つ以上を表すことができます。

-   *データ項目*ドライバーを送信または WMI クライアントから受信するデバイスに固有のデータを格納します。

-   *メソッド*(関数) ドライバーは、WMI クライアントに代わって実行します。

-   *イベント*ドライバーがデバイスに固有のイベントの通知を受信登録している WMI クライアントに送信します。

WMI データ ブロックは、として指定*WMI クラス*.mof ファイルにします。 各 WMI データ ブロックは、GUID によって識別されます。

すべてのドライバーでは、自分のデバイス クラスに対する WMI を定義する標準の WMI データ ブロックをサポートする必要があります。 これらの WMI データ ブロックが定義されている*Wmicore.mof*します。

ドライバーでは、.mof ファイルに定義する WMI データのブロックもサポートできます。 定義およびカスタマイズされた WMI データ ブロックを発行する方法については、次のセクションを参照してください。

-   [WMI データとイベント ブロックの MOF 構文](https://msdn.microsoft.com/library/windows/hardware/ff556400)

-   [WMI データとイベント ブロックの設計](https://msdn.microsoft.com/library/windows/hardware/ff543036)

-   [WMI スキーマの公開](https://msdn.microsoft.com/library/windows/hardware/ff559963)

-   [WMI プロパティ シート](https://msdn.microsoft.com/library/windows/hardware/ff566368)

### <a name="framework-wmi-objects-and-callback-functions"></a>Framework の WMI オブジェクトとコールバック関数

フレームワークは、ドライバーは、WMI データ プロバイダーを実装するために使用できる 2 つのオブジェクトを定義します。 *WMI プロバイダー オブジェクト*ドライバーを提供する WMI データ ブロックのスキーマを表します。 *WMI インスタンス オブジェクト*特定のプロバイダーに関連付けられているデータ ブロックのインスタンスを表します。 ドライバーは、これら 2 つのオブジェクトを定義する次のイベントのコールバック関数を実装することで、WMI クライアントと通信します。

<a href="" id="evtwmiproviderfunctioncontrol"></a>[*EvtWmiProviderFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff541855)  
有効にし、WMI データの収集および WMI イベントの送信用のドライバーのサポートを無効にします。

<a href="" id="evtwmiinstancequeryinstance"></a>[*EvtWmiInstanceQueryInstance*](https://msdn.microsoft.com/library/windows/hardware/ff541843)  
WMI プロバイダーのインスタンスのデータを WMI クライアントに配信します。

<a href="" id="evtwmiinstancesetinstance-and-evtwmiinstancesetitem"></a>[*EvtWmiInstanceSetInstance* ](https://msdn.microsoft.com/library/windows/hardware/ff541847)と[ *EvtWmiInstanceSetItem*](https://msdn.microsoft.com/library/windows/hardware/ff541852)  
クライアントが指定した値に、ドライバーのデータ ブロック内の情報を設定します。

<a href="" id="evtwmiinstanceexecutemethod"></a>[*EvtWmiInstanceExecuteMethod*](https://msdn.microsoft.com/library/windows/hardware/ff541836)  
クライアントの要求で、ドライバーによって提供されるメソッドを実行します。

### <a name="sample-drivers-that-implement-wmi"></a>WMI を実装しているサンプル ドライバー

FIREFLY、PCIDRV、およびトースター[サンプル ドライバー](sample-kmdf-drivers.md) WMI のデータ プロバイダーします。

 

 





