---
title: KS ピン
description: KS ピン
ms.assetid: 04d0d17b-c326-417d-b2e8-58b33420455a
keywords:
- ストリーミング ピン WDK カーネル
- KS ピンのストリーミング、KS ピン WDK カーネル
- KSPIN_DESCRIPTOR
- IRP ソース ピン WDK カーネル ストリーミング
- データ ソースのピン WDK カーネルのストリーミング
- 接続の WDK カーネルのストリーミングをピン留め
- カーネルの WDK、ピンのストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b33065b11f048d781b815f8d6add44bf08889018
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539652"
---
# <a name="ks-pins"></a>KS ピン





ミニドライバーに用意されている、 [ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)暗証番号 (pin) をインスタンス化の種類ごとに構造体。 暗証番号 (pin) の記述子構造体は、暗証番号 (pin) ファクトリと呼ばれます。 各ピン ファクトリは、特定の種類の 1 つ以上の暗証番号 (pin) のインスタンスをインスタンス化できます。 ファクトリ ピン留めするにはには、この記述子のインスタンス化するピンの型を記述する複数の配列が含まれています。

この記述子で作成したピンに属している 1 つまたは複数の KS カテゴリを指定する、ミニドライバー、**カテゴリ**KSPIN のメンバー\_記述子。 KS では、カテゴリを使用して、フィルターのグラフを作成するときに暗証番号 (pin) のインスタンスを接続します。 [ **KSPROPERTY\_トポロジ\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff565799)ドライバーがサポートする機能のカテゴリの配列のプロパティのクエリ。

ミニドライバーは、1 つまたは複数の pin デバイス名を登録する INF ファイルを提供します。 インストール時は、オペレーティング システムは、システム レジストリに名前と対応するカテゴリを読み込みます。 クライアントは、ピンをインスタンス化するこれらのデバイス名を持つファイルの作成の呼び出しを作成できます。

ユーザー モードのクライアントが Win32 関数を呼び出す[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)デバイスの名前に置き換えます。 たとえば、"*\\\\.\\フィルター\\オーディオ\\レンダラーの既定*"既定の出力のように構成されたオーディオ デバイスへのリンクにする可能性があります。 カーネル モードのクライアント呼び出し[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)カーネル モードから。 KS クライアントが通信をピン留めするインスタンスにファイルの作成のルーチンは、ファイル ハンドルを返した後[KS プロパティ](ks-properties.md)します。

暗証番号 (pin) の記述子構造体で、ミニドライバーの配列をレイアウト[ **KSPIN\_インターフェイス**](https://msdn.microsoft.com/library/windows/hardware/ff563537)構造体と[ **KSPIN\_MEDIUM**](https://msdn.microsoft.com/library/windows/hardware/ff563538)構造体を指定する、[インターフェイス](ks-interfaces.md)と[メディア](ks-mediums.md)pin ファクトリによってサポートされています。 [**KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)も、ミニドライバーがこのファクトリによって作成された pin の有効なデータ範囲を指定します。 これはの配列へのポインターを提供することで、 [ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)構造体。 ミニドライバーは、この暗証番号 (pin) ファクトリによって作成された新しいピンについてのデータとの通信のフローの方向も指定します。

ミニドライバーをサポートすることでピン留めするファクトリの実行時の探索を有効に、 [KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)プロパティ セット。

暗証番号 (pin) の接続を作成するには、 [ **KsCreatePin** ](https://msdn.microsoft.com/library/windows/hardware/ff561652)ルーチン。 この呼び出しで、ミニドライバーの型の構造体にポインターを渡します[ **KSPIN\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff563531)要求された接続をについて説明します。 Pin が作成されると、フィルターには、そのフィルターのファイル オブジェクトの下位のファイル オブジェクトとして新しい暗証番号 (pin) が表示されます。

ミニドライバー呼び出し[ **KsValidateConnectRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff567227)結果として得られる IRP で提供される記述子構造体を持つ\_MJ\_作成します。 このルーチンは、これらの構造を検証し、接続の構造とファイルのルート オブジェクトにポインターを返します。

ミニドライバーを使用して、**データフロー**と**通信**のメンバー [ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)構造体を定義する、次の pin 設定:

-   **IRP シンク暗証番号 (pin) と IRP ソース暗証番号 (pin)**

    *IRP ソース*pin Irp の問題は*IRP シンク*暗証番号 (pin) を受信します。 ユーザー モードのクライアントでは、関連するファイル ハンドルを使用して、IRP シンクの pin に直接 I/O 要求を送信します。 クライアントを使用して、 [ **KSPROPERTY\_PIN\_通信**](https://msdn.microsoft.com/library/windows/hardware/ff565194)または暗証番号 (pin) 型からのデータ フローするかどうかを確認します。

-   **データ シンクの暗証番号 (pin) とデータ ソースのピン留め**

    A*データ ソース*暗証番号 (pin) は、出力ピンをフィルターで、*データ シンク*pin が入力のピン留めします。 データ ソースまたはシンクのプロパティは、IRP のソースまたはシンクをされている依存しません。 たとえば、クライアントは IRP IRP ソース暗証番号 (pin)、データ シンクにピン留めするシンクのデータ ソースに接続できます。 クライアントを使用して、 [ **KSPROPERTY\_PIN\_データフロー** ](https://msdn.microsoft.com/library/windows/hardware/ff565197)または暗証番号 (pin) 型からのデータ フローするかどうかを確認します。

接続を終了するには、基になるファイル オブジェクトが破棄される前に、このソースの暗証番号 (pin) のハンドルを閉じてください。 ソースの暗証番号 (pin) は、シンクの暗証番号 (pin) によって提供されるリソースに依存する場合は、接続が終了したときに、ソースに通知するシンク暗証番号 (pin) の役割です。

クライアントと対話暗証番号 (pin) を呼び出すことでストリーミング カーネル、 **DeviceIoControl** (Microsoft Windows SDK のドキュメントで説明) ルーチンに[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)します。 呼び出し元に配置された I/O 制御コードによってその要求を識別する**Parameters.DeviceIoControl.IoControlCode** I/O スタックの場所の構造体。

要求をサポートするために、ミニドライバーはへのポインターを提供する[ **KSDISPATCH\_テーブル**](https://msdn.microsoft.com/library/windows/hardware/ff561723)構造体への呼び出しで[ **KsAllocateObjectHeader**](https://msdn.microsoft.com/library/windows/hardware/ff560972).

書き込み要求の配列へのポインターを含む[ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)をさらにデータのストリームへのポインターを含む構造体。 読み取り要求には、読み取りデータを返す必要がある空のヘッダーの構造体の配列へのポインターが含まれます。

 

 




