---
title: WMI データをサポートしているブロックと、ドライバー内のイベント
description: WMI データをサポートしているブロックと、ドライバー内のイベント
ms.assetid: a5138413-3ec4-4c61-9f00-6604759532e9
keywords:
- WMI の WDK KMDF、データのブロック
- WMI の WDK KMDF、イベント
- WMI データ ブロック WDK KMDF の読み取り/書き込み
- 読み取り専用の WMI データ ブロックの WDK KMDF
- WDK KMDF、WMI のイベント
- WDK KMDF のトレース
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8c7d7afa07cdf99c914920618fc117043e56af8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528374"
---
# <a name="supporting-wmi-data-blocks-and-events-in-your-driver"></a>WMI データをサポートしているブロックと、ドライバー内のイベント


\[KMDF にのみ適用されます。\]

フレームワーク ベースのドライバーでは、イベントのコールバック関数を提供することで WMI データ ブロックをサポートします。 ドライバーは、イベントを WMI クライアントに送信するオブジェクトのメソッドを呼び出すことによって WMI イベントをサポートします。

### <a href="" id="supporting-read-write-wmi-data-blocks"></a> WMI データ ブロックの読み取り/書き込みをサポートしています。

WMI データ ブロック内の情報が読み取り可能で、WMI クライアントが書き込み可能な場合は、ドライバーが提供する必要があります、 [ *EvtWmiInstanceQueryInstance* ](https://msdn.microsoft.com/library/windows/hardware/ff541843)サービス クライアントのコールバック関数の読み取り要求、plus [ *EvtWmiInstanceSetInstance* ](https://msdn.microsoft.com/library/windows/hardware/ff541847)または[ *EvtWmiInstanceSetItem* ](https://msdn.microsoft.com/library/windows/hardware/ff541852)サービスをコールバック関数 (または両方)、クライアントの要求を記述します。

ドライバーが提供する必要がありますも、データ ブロックにドライバーは、クライアントの要求で実行するメソッドが含まれている場合、 [ *EvtWmiInstanceExecuteMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff541836)コールバック関数。

WMI データ ブロックが書き込み専用の場合 (つまり、WMI クライアント情報をデータ ブロックに書き込むことができますが、データ ブロックを読み取ることができません)、ドライバーが提供されない、 [ *EvtWmiInstanceQueryInstance* ](https://msdn.microsoft.com/library/windows/hardware/ff541843)コールバック関数。

### <a href="" id="supporting-read-only-wmi-data-blocks"></a> 読み取り専用の WMI データ ブロックをサポートしています。

WMI データ ブロックの情報は、WMI クライアントによって変更できない場合、ドライバーが提供されない[ *EvtWmiInstanceSetInstance* ](https://msdn.microsoft.com/library/windows/hardware/ff541847)または[ *EvtWmiInstanceSetItem*](https://msdn.microsoft.com/library/windows/hardware/ff541852)コールバック関数。 WMI クライアントからのデータ ブロックの情報の要求をサポートするために、ドライバーは、次のいずれかを実行できます。

-   提供、 [ *EvtWmiInstanceQueryInstance* ](https://msdn.microsoft.com/library/windows/hardware/ff541843) WMI が指定したバッファーにドライバーが提供するデータをコピーするコールバック関数。

-   WMI インスタンス オブジェクトのデータ ブロックの情報を格納[コンテキスト領域](framework-object-context-space.md)、設定、 **UseContextForQuery**のインスタンスのメンバー [ **WDF\_WMI\_インスタンス\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff553058)構造体を**TRUE**します。

ドライバーが設定されている場合**UseContextForQuery**に**TRUE**フレームワークは、WMI クライアント インスタンスの情報を要求すると、WMI が指定したバッファーにインスタンス オブジェクトのコンテキストの領域をコピーします。 いいえ*EvtWmiInstanceXxx*ドライバーには、そのオブジェクト コンテキストの領域からの読み取り専用の固定長のデータを提供する 1 つの WMI インスタンスのみが含まれている場合は、コールバックが必要です。

ドライバーを提供できますも読み取り専用データ ブロックにドライバーは、クライアントの要求で実行するメソッドが含まれている場合、 [ *EvtWmiInstanceExecuteMethod* ](https://msdn.microsoft.com/library/windows/hardware/ff541836)コールバック関数。

### <a name="supporting-expensive-wmi-data-blocks"></a>高価な WMI データ ブロックをサポートしています。

ドライバーは、その WMI データ ブロックの 1 つをサポートする比較的大量の動的なデータを収集し、ドライバーが、次の操作にする必要があります。

-   設定して「コスト」するデータ ブロックを宣言、 **WdfWmiProviderExpensive**フラグ、**フラグ**WMI プロバイダー オブジェクトのメンバー [ **WDF\_WMI\_プロバイダー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff553067)構造体。

-   提供、 [ *EvtWmiProviderFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541855)コールバック関数を有効にし、データのブロック、または呼び出しのデータ収集を無効にします[ **WdfWmiProviderIsEnabled。** ](https://msdn.microsoft.com/library/windows/hardware/ff551200)ドライバーが有効にする必要がありますまたはデータの収集を無効にするかどうかを判断します。

ドライバーが設定されている場合、 **WdfWmiProviderExpensive**フラグ、フレームワークによって、 [ *EvtWmiProviderFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541855)を WMI クライアントの登録時にコールバック関数データ ブロックにアクセスします。 コールバック関数には、データを収集するドライバーの機能が有効にする必要があります。 WMI のすべてのクライアントは、データ ブロックの登録を削除する場合、フレームワーク、 *EvtWmiProviderFunctionControl*コールバック関数を再度、ドライバーはデータ収集を停止できるようにします。

### <a name="supporting-wmi-events"></a>対応する WMI イベント

ドライバーは、例外的な条件の WMI クライアントに通知するのに WMI イベントを使用できます。 (する必要がありますいないイベントを使用する WMI エラーのログ記録する代わりにします。)データ項目のように、WMI イベントは、管理オブジェクト フォーマット (.mof) ファイル内で WMI データ ブロックで定義されます。

WMI クライアントは、WMI イベントの通知を登録します。 に登録されている WMI クライアントを、イベントを送信するには、ドライバーを呼び出し、 [ **WdfWmiInstanceFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff551182)メソッド。 このメソッドは、必要に応じて、クライアントにイベント固有のデータを送信するドライバーを使用します。

イベントを定義する WMI データ ブロックには、WMI データ項目またはメソッドの項目も含まれています、ドライバーは、適切な WMI のコールバック関数を提供します。 データ ブロックでイベントを定義している場合、データまたはメソッドのアイテムが含まれていないには、ドライバーを設定する必要があります、 **WdfWmiProviderEventOnly**フラグ、**フラグ**WMI プロバイダー オブジェクトのメンバー [ **WDF\_WMI\_プロバイダー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff553067)構造体。

ドライバーを呼び出す必要があります[ **WdfWmiInstanceFireEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff551182)を WMI クライアントがイベント通知に登録されている場合にのみです。 ドライバーを調べるかどうかは呼び出す必要があります**WdfWmiInstanceFireEvent**指定するかによって、 [ *EvtWmiProviderFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541855)コールバック関数または呼び出し[**WdfWmiProviderIsEnabled**](https://msdn.microsoft.com/library/windows/hardware/ff551200)します。

### <a name="supporting-wmi-event-tracing"></a>WMI イベントのトレースをサポートしています。

トレース イベントは、その他の WMI イベントと同様に、.mof ファイルで定義されます。 ドライバーは、トレース イベントの WMI プロバイダー オブジェクトを作成するときに設定する必要があります、 **WdfWmiProviderTracing**フラグ、**フラグ**プロバイダー オブジェクトのメンバー [ **WDF\_WMI\_プロバイダー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff553067)構造体。

プロバイダーのインスタンスが登録されたら、ドライバーを呼び出すことが[ **WdfWmiProviderGetTracingHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff551198)トレース ハンドルを取得します。 ドライバーは、トレースのハンドルを使用してへの入力として、 [ **WmiTraceMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff565836)ルーチン。

イベントのトレースの詳細についてを参照してください。

-   [WMI イベントのトレース](https://msdn.microsoft.com/library/windows/hardware/ff566350)

-   [WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)

 

 





