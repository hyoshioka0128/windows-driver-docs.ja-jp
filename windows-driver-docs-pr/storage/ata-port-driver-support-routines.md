---
title: ATA ポートドライバーのサポートルーチン
description: ATA ポートドライバーのルーチンについて説明します。
ms.assetid: 59222e82-8abb-4ef6-b58d-f70470c2def0
keywords:
- ATA ドライバーのサポートルーチン
- ストレージ WDK
- ストレージサポートルーチン
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: b4c32831f8a3c324eeb648549220f0fb3d02e80d
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72256322"
---
# <a name="ata-port-driver-support-routines"></a>ATA ポートドライバーのサポートルーチン

このページでは、システム指定の ATA ポートドライバーによって提供されるサポートルーチンを分類します。

ATA ドライバーミニポートルーチンの一覧については、「 [Ata ミニポートドライバー](ata-miniport-drivers.md)」を参照してください。

## <a name="initialization-routine"></a>初期化ルーチン

ATA ポートドライバーは、次の初期化ルーチンを提供します。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortInitializeEx** | ポートとミニポートドライバーを初期化します。 |

## <a name="routines-for-pci-config-space-access"></a>PCI 構成領域アクセスのルーチン

ATA ポートドライバーには、デバイスの PCI 構成領域の内容を読み取って変更するための次のルーチンが用意されています。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortGetBusData** | デバイスの PCI 構成領域内の指定された場所からデータを取得します。 |
| **AtaPortSetBusData** | 指定されたデバイスの PCI 構成領域にあるデータを、指定したオフセット位置に格納します。 |
|

## <a name="routines-for-processing-io-requests"></a>I/o 要求を処理するためのルーチン

ATA ポートドライバーは、次の i/o 要求処理サポートルーチンを提供します。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortGetScatterGatherList** | この要求に関連付けられているスキャッター/ギャザーリストを取得します。 |
| **AtaPortGetPhysicalAddress** | 仮想アドレスの範囲を物理アドレスの範囲に変換します。 |
| **AtaPortGetDeviceBase** | ホストバスアダプター (HBA) との通信に使用される、マップされた論理ベースアドレスを返します。 |
| **AtaPortGetUncachedExtension** | CPU およびデバイスによって共有される、キャッシュされていない共通バッファーを割り当てます。 |
| **AtaPortBuildRequestSenseIrb** | 操作コード SCSIOP_REQUEST_SENSE の IRB を構築して返します。 |
| **AtaPortReleaseRequestSenseIrb** | **AtaPortBuildRequestSenseIrb**を使用して割り当てられた REQUEST sense IRB を解放します。 |
| **AtaPortCompleteAllActiveRequests** | 指定されたデバイスのすべてのアクティブな IRBs を完了します。 |
| **AtaPortCompleteRequest** | 指定された IRB を完了します。 |

## <a name="callback-routines"></a>コールバックルーチン

ミニポートドライバーは、いくつかのルーチンを使用して、ポートドライバーからのコールバックを要求します。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortRequestWorkerRoutine** | ワーカールーチンを要求します。 |
| **AtaPortRequestSynchronizedRoutine** | 中断サービスルーチン (ISR) との同期を要求します。 |
| **AtaPortControllerSyncRoutine** | コントローラー上のすべてのチャネル間で共有されるデータ構造への同期アクセスを提供します。 |
| **AtaPortRequestTimer** | タイマーコールバックを要求します。 |

## <a name="routines-that-report-a-configuration-change"></a>構成の変更を報告するルーチン

次のルーチンを使用すると、ミニポートドライバーは、チャネルに接続されているデバイスの構成に対する変更を ATA ポートドライバーに通知できます。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortBusChangeDetected** | 指定されたチャネルのデバイス構成の変更をポートドライバーに通知します。 |
| **AtaPortRequestPowerStateChange** | 指定されたデバイスの電源状態の移行を要求します。 |

## <a name="routines-to-control-request-queues"></a>要求キューを制御するルーチン

ポートドライバーは、各チャネルにつき1つの論理ユニット番号 (LUN) 要求キューと1つの要求キューを保持します。 ミニポートドライバーは、次のルーチンを使用して、さまざまな要求キューを一時停止および再開できます。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortDeviceBusy** | 指定されたデバイスがビジー状態であることをポートドライバーに通知します。 |
| **AtaPortDeviceReady** | 指定されたデバイスが新しい要求を受け入れる準備ができていることをポートドライバーに通知します。 |

## <a name="utility-routines"></a>ユーティリティルーチン

次のルーチンは、ミニポートドライバー用の一般的なユーティリティサポート機能です。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortCopyMemory** | ある場所から別の場所にデータをコピーします。 |
| \* * AtaPortMoveMemory ルーチン | ある場所から別の場所にデータをコピーします。 |
| **AtaPortConvertUlongToPhysicalAddress** | 指定された ULONG アドレスを IDE_PHYSICAL_ADDRESS 型の値に変換します。 |
| **AtaPortConvertPhysicalAddressToUlong** | IDE_PHYSICAL_ADDRESS 型のアドレスを ULONG に切り捨てます。 |
| **AtaPortStallExecution** | ミニポートドライバーの停止。 |
| **AtaPortInitializeQueueTag** | 指定されたデバイスのキュータグリストを初期化します。 |
| **AtaPortAllocateQueueTag** | 指定されたデバイスのキュータグを返します。 |
| **AtaPortReleaseQueueTag** | 指定されたキュータグを解放します。 |

## <a name="debug-and-error-reporting-routines"></a>デバッグとエラー報告ルーチン

次のルーチンは、デバッグおよびエラー報告に使用できます。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortDebugPrint** | デバッガーが出力するためのメッセージ文字列をカーネルデバッガーに渡します。 |

## <a name="routines-for-device-port-and-register-access"></a>デバイスポートのルーチンとアクセスの登録

ATA ポートドライバーは、次のポートを提供し、アクセスのサポートルーチンを登録します。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortReadPortBufferUchar** | 指定された数の符号なしバイト値を HBA からバッファーに転送します。 |
| **AtaPortReadPortBufferUlong** | 指定された数の ULONG 値を HBA からバッファーに転送します。 |
| **AtaPortReadPortBufferUshort** | 指定された数の USHORT 値を HBA からバッファーに転送します。 |
| **AtaPortReadPortUchar** | HBA から符号なしバイト値を読み取ります。 |
| **AtaPortReadPortUlong** | HBA から ULONG 値を読み取ります。 |
| **AtaPortReadPortUshort** | HBA から USHORT 値を読み取ります。 |
| **AtaPortReadRegisterBufferUchar** | 指定された数の符号なしバイトを HBA からバッファーに転送します。 |
| **AtaPortReadRegisterBufferUlong** | 指定された数の ULONG を HBA からバッファーに転送します。 |
| **AtaPortReadRegisterBufferUshort** | 指定された数の USHORT を HBA からバッファーに転送します。 |
| **AtaPortReadRegisterUchar** | HBA から符号なしバイト値を読み取ります。 |
| **AtaPortReadRegisterUlong** | HBA から ULONG 値を読み取ります。 |
| **AtaPortReadRegisterUshort** | HBA から USHORT 値を読み取ります。 |
| **AtaPortWritePortBufferUchar** | 指定したレジスタアドレスに値を書き込みます。 |
| **AtaPortWritePortBufferUlong** | 指定したレジスタアドレスに値を書き込みます。 |
| **AtaPortWritePortBufferUshort** | 指定したレジスタアドレスに値を書き込みます。 |
| **AtaPortWritePortUchar** | 署名されていないバイト値を HBA に転送します。 |
| **AtaPortWritePortUlong** | ULONG 値を HBA に転送します。 |
| **AtaPortWritePortUshort** | USHORT 値を HBA に転送します。 |
| **AtaPortWriteRegisterBufferUchar** | バッファーから指定された数の符号なしバイトを HBA に転送します。 |
| **AtaPortWriteRegisterBufferUlong** | 指定された数の ULONG 値をバッファーから HBA に転送します。 |
| **AtaPortWriteRegisterBufferUshort** | 指定された数の USHORT 値をバッファーから HBA に転送します。 |
| **AtaPortWriteRegisterUchar** | HBA アドレスに符号なしバイトを転送します。 |
| **AtaPortWriteRegisterUlong** | ULONG 値を HBA アドレスに転送します。 |
| **AtaPortWriteRegisterUshort** | USHORT 値を HBA アドレスに転送します。|

## <a name="routines-for-registry-access"></a>レジストリアクセスのルーチン

チャネルインターフェイスを実装するミニポートドライバーは、次のルーチンを呼び出して Windows レジストリにアクセスできます。 コントローラーインターフェイスルーチンのみを実装するミニポートドライバーは、これらのルーチンにアクセスできません。

| ルーチン | 説明 |
| ------- | ----------- |
| **AtaPortRegistryAllocateBuffer** | レジストリ操作用のバッファーを割り当てます。 |
| **AtaPortRegistryFreeBuffer** | **AtaPortRegistryAllocateBuffer**を使用して割り当てられたレジストリバッファーを解放します。 |
| **AtaPortRegistryControllerKeyRead** | 指定された値の名前に関連付けられているデータを読み取るレジストリキー HKLM @ no__t-0CurrentControlSet @ no__t-1Services @ no__t-2 @ no__t-3service name @ no__t-4\Controller*n*( *N*はコントローラーの番号)。 |
| **AtaPortRegistryContrlollerKeyWrite** | は、指定された値の名前に、レジストリキー HKLM @ no__t-0CurrentControlSet @ no__t-1Services @ no__t-2 @ no__t-3service name @ no__t-4\Controller*N*に書き込みます。ここで、 *N*はコントローラーの番号です。 |
| **AtaPortRegistryControllerKeyWriteDeferred** | は、指定された値の名前に、レジストリキー HKLM @ no__t-0CurrentControlSet @ no__t-1Services @ no__t-2 @ no__t-3service name @ no__t-4\Controller*N*にデータを非同期的に書き込みます。ここで、 *N*はコントローラーの番号です。 |
| **AtaPortRegistryChannelSubKeyRead** | は、指定された値名に関連付けられているデータを読み取ります。レジストリキー HKLM @ no__t-0CurrentControlSet @ no__t-1Services @ no__t-2 @ no__t-3service name @ no__t-4\Controller*N*\ Channel*M*,、 *N*はcontroller と*M*は、チャネルの番号です。 |
| **AtaPortRegistryChannelSubKeyWrite** | は、レジストリキー HKLM @ no__t-0CurrentControlSet @ no__t-1Services @ no__t-2 @ no__t-3service name @ no__t-4\Controller*N*\ Channel*M*の下に、指定した値の名前にデータを書き込みます。ここで、 *N*はコントローラーと M の番号です。チャネルの番号を指定します。 |
| **AtaPortRegistryChannelSubKeyWriteDeferred** | は、指定された値の名前に、レジストリキー HKLM @ no__t-0CurrentControlSet @ no__t-1Services @ no__t-2 @ no__t-3service name @ no__t-4\Controller*N*\ Channel*M*の下にデータを非同期的に書き込みます。ここで、 *N*はcontroller と*M*は、チャネルの番号です。 |
