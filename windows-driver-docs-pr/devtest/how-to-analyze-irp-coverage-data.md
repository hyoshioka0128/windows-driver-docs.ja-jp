---
title: IRP カバレッジ データを分析する方法
description: IRP カバレッジ データを分析する方法
ms.assetid: 71b87948-8e69-4b4a-9546-ea27e96a4bf8
keywords:
- ドライバー カバレッジ Toolkit WDK は、データの分析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55bd5232a9881c70eb66a335386229a2e8019011
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356502"
---
# <a name="how-to-analyze-irp-coverage-data"></a>IRP カバレッジ データを分析する方法


**注**  ドライバーのカバレッジ Toolkit は Windows 10 で不要になったと、インストーラーが WDK に含まれていません。 ここで説明されている Windows 10 でタスクを実行する代わりに使用[Driver Verifier](driver-verifier.md)と[IRP のログ記録](irp-logging.md)します。

 

このトピックでは、IRP カバレッジ データを分析するのに役立つガイドラインを提供します。 IRP カバレッジ データを収集するためのガイドラインについては、次を参照してください。 [IRP カバレッジ データを収集する方法](how-to-collect-irp-coverage-data.md)します。

使用することができます、テスト コンピューターで 1 つまたは複数のデバイスの IRP のカバレッジ データを収集した後、[カバレッジのテスト (デバイスの基本)](coverage-tests--device-fundamentals-.md)にこのデータからレポートを作成します。 これらのレポートは、指定したデバイスのドライバー スタックを左または入力される個々 の I/O 要求パケット (Irp) の数を表示します。 入力またはドライバー スタックのままにしていない Irp の種類も報告されます。

このトピックでは、使用して、例として、テスト コンピューター上のデバイス ノード (devnode) が有効になっている IRP カバレッジ データから生成されたレポート。 Devnode は 9740、および IRP カバレッジ有効だった devnode を実行して、 **IRP を有効にするカバレッジ データ コレクション**テスト コンピューター上のツール。

WDK と Visual Studio のテスト環境の設定の詳細については、次を参照してください。 [Visual Studio を使用して実行時にドライバーをテストする方法を](https://docs.microsoft.com/windows-hardware/drivers)します。 選択して、テストとツールのパラメーターの構成については、次を参照してください。[を選択して、デバイスの基本テストを構成する方法](https://docs.microsoft.com/windows-hardware/drivers)と[デバイス基礎テスト パラメーター](https://docs.microsoft.com/windows-hardware/drivers)します。

この devnode IRP カバレッジ レポートを実行して生成 IRP のカバレッジ データを収集すると、**表示 IRP カバレッジ データを収集する**テスト コンピューター上のツール。

```
Drvcov /C 9740
```

IRP のカバレッジ レポートには、4 つのセクションがあります。

<span id="Report_Header_______"></span><span id="report_header_______"></span><span id="REPORT_HEADER_______"></span>**レポート ヘッダー**   
このセクションでは、IRP カバレッジ データが、レポートに表示されるデバイスに関する情報を提供します。

Devnode 9740 の IRP カバレッジ レポートは、以下に示します。

```
Getting coverage data
Data source
 Source Type:  Driver
 Source Name:  \\.\DrvcovControl1
 Device
   Friendly Name : Disk drive 
   Class Name    : DiskDrive 
   Device ID     : IDE\DISKST9320421AS_____________________________SD13____\5&37E07111&0&0.0.0 
   Device #      : 1 
 Devnode #     : 9740
```

<span id="IRP_Major__MJ__and_Minor__MN__Coverage_Data_______"></span><span id="irp_major__mj__and_minor__mn__coverage_data_______"></span><span id="IRP_MAJOR__MJ__AND_MINOR__MN__COVERAGE_DATA_______"></span>**IRP (MJ) メジャーおよびマイナー (MN) カバレッジ データ**   
ここでは、関数コード IRP の適用範囲期間中に、指定した devnode 用のドライバーによって処理される、IRP MJ とその下位 MN のカウンターを示します。 ドライバの対応 toolkit モニターと 52 IRP MJ および MJ 関数コードでのレポート。

ここでは、次の内容について説明します。

-   各 IRP MJ および mn の各カウンターには、ドライバーによって処理されるコードが機能します。 これらのカウンターは、どの Irp が十分なテスト カバレッジやカバレッジの拡大が必要な場合がありますを使用できます。

-   ドライバーによって処理されなかった IRP MJ および mn の各関数のコードの一覧。 この情報は非常に重要であり、コード カバレッジのテストでの欠陥について把握できます。

**注**  をテストするには、どの Irp に関する意思決定は、ドライバーとの Irp に依存、ドライバーがサポートされます。 IRP MJ および MN のカバレッジ データは、ドライバーのコード カバレッジのテストの効率性を評価するのに役立ちます。

 

Devnode 9740 の IRP MJ および MN のカバレッジ データは、次の例で示すように。

```
|--------------------------------------------------------|
| MJ & MN Device irp coverage                            |
|--------------------------------------------------------|
| IRPS covered     19                      |  # of times |
|--------------------------------------------------------|
| Unknown                                  |           5 | 
| PNP\QUERY_RESOURCE_REQUIREMENTS          |           3 | 
| PNP\FILTER_RESOURCE_REQUIREMENTS         |           3 | 
| PNP\START_DEVICE                         |           8 | 
| DEVICE_CONTROL                           |         293 | 
| READ                                     |        2543 | 
| PNP\QUERY_CAPABILITIES                   |           3 | 
| PNP\QUERY_PNP_DEVICE_STATE               |           7 | 
| CREATE                                   |          44 | 
| CLEANUP                                  |          45 | 
| CLOSE                                    |          43 | 
| WRITE                                    |        2488 | 
| WMI\REGINFO_EX                           |           5 | 
| WMI\REGINFO                              |           5 | 
| FLUSH_BUFFERS                            |        1491 | 
| PNP\QUERY_DEVICE_RELATIONS\Target        |          23 | 
| WMI\QUERY_ALL_DATA                       |           6 | 
| POWER\QUERY_POWER\SYSTEM                 |           2 | 
| SHUTDOWN                                 |           2 | 
|--------------------------------------------------------|
| IRPS NOT covered     33                  |             |
|--------------------------------------------------------|
| INTERNAL_DEVICE_CONTROL                  |             | 
| POWER\WAIT_WAKE                          |             | 
| POWER\SET_POWER\SYSTEM                   |             | 
| POWER\SET_POWER\DEVICE                   |             | 
| POWER\QUERY_POWER\DEVICE                 |             | 
| WMI\QUERY_SINGLE_INSTANCE                |             | 
| WMI\CHANGE_SINGLE_INSTANCE               |             | 
| WMI\CHANGE_SINGLE_ITEM                   |             | 
| WMI\ENABLE_EVENTS                        |             | 
| WMI\DISABLE_EVENTS                       |             | 
| WMI\ENABLE_COLLECTION                    |             | 
| WMI\DISABLE_COLLECTION                   |             | 
| WMI\EXECUTE_METHOD                       |             | 
| PNP\QUERY_REMOVE_DEVICE                  |             | 
| PNP\REMOVE_DEVICE                        |             | 
| PNP\CANCEL_REMOVE_DEVICE                 |             | 
| PNP\STOP_DEVICE                          |             | 
| PNP\QUERY_STOP_DEVICE                    |             | 
| PNP\CANCEL_STOP_DEVICE                   |             | 
| PNP\QUERY_DEVICE_RELATIONS\Bus           |             | 
| PNP\QUERY_DEVICE_RELATIONS\Eject         |             | 
| PNP\QUERY_DEVICE_RELATIONS\Removal       |             | 
| PNP\QUERY_INTERFACE                      |             | 
| PNP\QUERY_RESOURCES                      |             | 
| PNP\QUERY_DEVICE_TEXT                    |             | 
| PNP\READ_CONFIG                          |             | 
| PNP\WRITE_CONFIG                         |             | 
| PNP\EJECT                                |             | 
| PNP\SET_LOCK                             |             | 
| PNP\QUERY_ID                             |             | 
| PNP\QUERY_BUS_INFORMATION                |             | 
| PNP\DEVICE_USAGE_NOTIFICATION            |             | 
| PNP\SURPRISE_REMOVAL                     |             | 
|--------------------------------------------------------|
| Stats                                                  |
|--------------------------------------------------------|
| Total IRP count        :     52                        |
| Covered IRP count      :     19                        |
| NOT Covered IRP count  :     33                        |
| Covered IRP %          :     36.54%                    |
| NOT Covered IRP %      :     63.46%                    |
|--------------------------------------------------------|
```

<span id="IRP_MJ_Coverage_Data_______"></span><span id="irp_mj_coverage_data_______"></span><span id="IRP_MJ_COVERAGE_DATA_______"></span>**IRP MJ カバレッジ データ**   
ここでは、関数コード IRP の適用範囲期間中に、指定した devnode 用のドライバーによって処理される、IRP MJ のみのカウンターを示します。 ドライバの対応 toolkit モニターと 13 IRP MJ 関数コードでのレポート。

ここでは、次の内容について説明します。

-   ドライバーによって処理された各 IRP MJ 関数コードのカウンターです。 どの Irp が十分なテスト カバレッジやカバレッジの拡大が必要な場合がありますを決定する、これらのカウンターを使用することができます。

-   ドライバーによって処理されなかった IRP MJ 関数コードの一覧。 この情報は非常に重要であり、コード カバレッジのテストでの欠陥について把握できます。

IRP MJ および MN のカバレッジ データこのセクションではデータを使用するをコード カバレッジのテストの効率性を分析することができます。 具体的には、このデータは、各 IRP MJ 関数のコード用のドライバーのディスパッチ ルーチンがテストされた度合いを示しています。

Devnode 9740 の IRP MJ カバレッジ データは、次の例で示すように。

```
|--------------------------------------------------------|
| MJ Device irp coverage                                 |
|--------------------------------------------------------|
| IRPS covered     12                      |  # of times |
|--------------------------------------------------------|
| IRP_MJ_UNKNOWN                           |           1 | 
| IRP_MJ_PNP                               |           6 | 
| IRP_MJ_DEVICE_CONTROL                    |           1 | 
| IRP_MJ_READ                              |           1 | 
| IRP_MJ_CREATE                            |           1 | 
| IRP_MJ_CLEANUP                           |           1 | 
| IRP_MJ_CLOSE                             |           1 | 
| IRP_MJ_WRITE                             |           1 | 
| IRP_MJ_SYSTEM_CONTROL                    |           3 | 
| IRP_MJ_FLUSH_BUFFERS                     |           1 | 
| IRP_MJ_POWER                             |           1 | 
| IRP_MJ_SHUTDOWN                          |           1 | 
|--------------------------------------------------------|
| IRPS NOT covered      1                  |             |
|--------------------------------------------------------|
| IRP_MJ_INTERNAL_DEVICE_CONTROL           |             | 
|--------------------------------------------------------|
| Stats                                                  |
|--------------------------------------------------------|
| Total IRP count        :     13                        |
| Covered IRP count      :     12                        |
| NOT Covered IRP count  :      1                        |
| Covered IRP %          :     92.31%                    |
| NOT Covered IRP %      :      7.69%                    |
|--------------------------------------------------------|
```

<span id="IRP_Pairs_Coverage_Data_______"></span><span id="irp_pairs_coverage_data_______"></span><span id="IRP_PAIRS_COVERAGE_DATA_______"></span>**IRP のペアをカバレッジ データ**   
このセクションでは、IRP の適用範囲期間中に Irp のペアが devnode のドライバー スタック内で同時にアクティブな回数の合計が表示されます。 ドライバの対応 toolkit の監視とレポート 1099 異なる IRP のペアします。

このセクションでは、ドライバーによって同時に処理された MJ/MN 関数コードの場合は、各 IRP MJ のカウンターが表示されます。 これらのカウンターは、どの Irp が十分なテスト カバレッジやカバレッジの拡大が必要な場合がありますを使用できます。

他の種類、IRP カバレッジ データのこのセクションではデータを使用すると、コード カバレッジのテストの効率性を分析することができます。 ただし、このデータは大幅に異なるドライバーが IRP の同時実行のテストがどの程度が表示を処理します。

Devnode 9740 の IRP のペアのカバレッジ データは、次の例で示すように。

```
|--------------------------------------------------------|
| MJ & MN Device IRP Concurrency pairs.                  |
|--------------------------------------------------------|
| IRP Pairs covered                     25 |  # of times |
|--------------------------------------------------------|
| CREATE                                   |             | 
| READ                                     |          10 | 
|--------------------------------------------------------|
| CREATE                                   |             | 
| WRITE                                    |           5 | 
|--------------------------------------------------------|
| CREATE                                   |             | 
| DEVICE_CONTROL                           |           4 | 
|--------------------------------------------------------|
| CLOSE                                    |             | 
| READ                                     |          10 | 
|--------------------------------------------------------|
| CLOSE                                    |             | 
| WRITE                                    |           4 | 
|--------------------------------------------------------|
| CLOSE                                    |             | 
| DEVICE_CONTROL                           |           4 | 
|--------------------------------------------------------|
| READ                                     |             | 
| READ                                     |        1513 | 
|--------------------------------------------------------|
| READ                                     |             | 
| WRITE                                    |        1498 | 
|--------------------------------------------------------|
| READ                                     |             | 
| FLUSH_BUFFERS                            |         929 | 
|--------------------------------------------------------|
| READ                                     |             | 
| DEVICE_CONTROL                           |          68 | 
|--------------------------------------------------------|
| READ                                     |             | 
| CLEANUP                                  |          11 | 
|--------------------------------------------------------|
| READ                                     |             | 
| POWER\QUERY_POWER\SYSTEM                 |           1 | 
|--------------------------------------------------------|
| READ                                     |             | 
| WMI\QUERY_ALL_DATA                       |           2 | 
|--------------------------------------------------------|
| READ                                     |             | 
| PNP\QUERY_DEVICE_RELATIONS\Target        |           7 | 
|--------------------------------------------------------|
| READ                                     |             | 
| PNP\QUERY_PNP_DEVICE_STATE               |           1 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| WRITE                                    |        1448 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| FLUSH_BUFFERS                            |         852 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| DEVICE_CONTROL                           |           8 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| CLEANUP                                  |           4 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| PNP\QUERY_DEVICE_RELATIONS\Target        |           1 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| PNP\QUERY_PNP_DEVICE_STATE               |           2 | 
|--------------------------------------------------------|
| FLUSH_BUFFERS                            |             | 
| FLUSH_BUFFERS                            |          27 | 
|--------------------------------------------------------|
| FLUSH_BUFFERS                            |             | 
| DEVICE_CONTROL                           |           1 | 
|--------------------------------------------------------|
| DEVICE_CONTROL                           |             | 
| CLEANUP                                  |           7 | 
|--------------------------------------------------------|
| DEVICE_CONTROL                           |             | 
| PNP\START_DEVICE                         |           2 | 
|--------------------------------------------------------|
|--------------------------------------------------------|
| Stats                                                  |
|--------------------------------------------------------|
| Total IRP pairs                 :        1099          |
| Covered IRP pairs               :          25          |
| NOT Covered IRP pairs           :        1074          |
| Covered IRP pairs %             :           2.27%      |
| NOT Covered IRP pairs %         :          97.73%      |
|--------------------------------------------------------|
```

 

 





