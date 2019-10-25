---
title: KS ピン
description: KS ピン
ms.assetid: 04d0d17b-c326-417d-b2e8-58b33420455a
keywords:
- WDK カーネルストリーミングをピン留めする
- KS では、WDK カーネルストリーミング、約 KS ピンをピン留めします。
- KSPIN_DESCRIPTOR
- IRP ソース pin WDK カーネルストリーミング
- データソースの pin WDK カーネルストリーミング
- ピン接続の WDK カーネルストリーミング
- カーネルストリーミング WDK、pin
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac1482676e18168223bc5b7765c8a74ccacac67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842507"
---
# <a name="ks-pins"></a>KS ピン





ミニドライバーは、インスタンス化する pin の種類ごとに[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造体を提供します。 Pin 記述子の構造体は、ピンファクトリと呼ばれます。 各ピンファクトリは、特定の種類の1つ以上の pin インスタンスをインスタンス化できます。 ピンファクトリには、この記述子がインスタンス化する pin の種類を記述する配列がいくつか含まれています。

ミニドライバーは、この記述子によって作成されるピンが KSPIN\_記述子の**カテゴリ**メンバーに属する1つ以上の KS カテゴリを指定します。 は、カテゴリを使用して、フィルターグラフを構築するときにピンインスタンスを接続します。 [**Ksk プロパティ\_TOPOLOGY\_categories**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)プロパティは、ドライバーがサポートする機能カテゴリの配列を照会します。

ミニドライバーには、1つまたは複数のピンデバイス名を登録する INF ファイルが用意されています。 インストール時に、オペレーティングシステムによって、名前と対応するカテゴリがシステムレジストリに読み込まれます。 クライアントは、これらのデバイス名を使用してファイルの作成呼び出しを行い、pin をインスタンス化できます。

ユーザーモードクライアントは、デバイスの名前を使用して Win32 関数[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出します。 たとえば、" *\\\\です。\\フィルター\\オーディオ\\既定のレンダラー*) は、既定の出力用に構成されているオーディオデバイスへのリンクにすることができます。 カーネルモードクライアントは、カーネルモードから[**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)を呼び出します。 ファイルの作成ルーチンによってファイルハンドルが返された後、KS クライアントは[Ks プロパティ](ks-properties.md)を使用して、pin インスタンスと通信します。

ピン記述子構造体では、ミニドライバーは、そのピンファクトリによってサポートされる[インターフェイス](ks-interfaces.md)と[メディア](ks-mediums.md)を指定する[**kspin\_インターフェイス**](https://docs.microsoft.com/previous-versions/ff563537(v=vs.85))構造体と[**kspin\_中程度**](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))の構造体の配列をレイアウトします。 [**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)も、ミニドライバーが、そのファクトリによって作成されるピンの有効なデータ範囲を指定します。 これを行うには、 [**Ksdatarange**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))体の配列へのポインターを指定します。 また、ミニドライバーは、この pin ファクトリによって作成される新しい pin のデータと通信フローの方向を指定します。

ミニドライバーは、 [Kspropsetid\_pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)プロパティセットをサポートすることにより、pin ファクトリの実行時検出を有効にします。

Pin 接続を作成するには、 [**KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)ルーチンを呼び出します。 この呼び出しでは、ミニドライバーは、要求された接続を記述する[**Kspin\_CONNECT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)型の構造体へのポインターを渡します。 Pin を作成すると、そのフィルターのファイルオブジェクトの下位にあるファイルオブジェクトとして新しい pin が表示されます。

ミニドライバーは[**KsValidateConnectRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksvalidateconnectrequest)を呼び出し、結果として得られる IRP\_MJ\_CREATE に指定された記述子構造を使用します。 このルーチンは、これらの構造を検証し、接続構造体とルートファイルオブジェクトへのポインターを返します。

ミニドライバーは、 [**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造体のデータ**フロー**と**通信**メンバーを使用して、次の pin の詳細を定義します。

-   **IRP ソースピンと IRP シンク pin**

    *Irp ソース*ピンは、irp を発行します。*IRP シンク*ピンはそれらを受け取ります。 ユーザーモードのクライアントは、関連するファイルハンドルを通じて IRP シンク pin に直接 i/o 要求を送信します。 クライアントは、Ksk プロパティを使用して[ **\_通信\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-communication)留めし、データが pin の種類に出入りするかどうかを確認します。

-   **データソースピンとデータシンク pin の比較**

    *データソース*の pin は、フィルターの出力ピンです。*データシンク*の pin は入力ピンです。 データソースまたはシンクになるのプロパティは、IRP のソースまたはシンクとは独立しています。 たとえば、クライアントはデータソース、IRP シンク pin をデータシンク、IRP ソース pin に接続できます。 クライアントは、Ksk プロパティを使用して\_データフローを[ **\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataflow)留めし、データが pin の種類に出入りするかどうかをチェックします。

接続を終了するときは、基になるファイルオブジェクトが破棄される前に、ソースピンのハンドルを閉じる必要があります。 ソース pin がシンク pin によって提供されるリソースに依存している場合、接続が終了したときにソースに通知するのはシンク pin の役割です。

クライアントは、 [**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)を使用して**DeviceIoControl**ルーチン (Microsoft Windows SDK ドキュメントに記述されています) を呼び出すことによって、カーネルストリーミングピンと対話します。 呼び出し元は i/o の制御コードによって要求を識別します。 i/o の制御コードは、i/o スタックの場所構造の**DeviceIoControl**に配置します。

要求をサポートするために、ミニドライバーは[**KsAllocateObjectHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksallocateobjectheader)の呼び出しで[**KSK ディスパッチ\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdispatch_table)構造へのポインターを提供します。

書き込み要求には、 [**Ksk ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)構造体の配列へのポインターが含まれています。これにはストリームデータへのポインターが含まれています。 読み取り要求には、読み取りデータを返す必要がある空のヘッダー構造の配列へのポインターが含まれています。

 

 




