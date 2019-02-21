---
title: ドライバーのカバレッジ Toolkit の概要
description: ドライバーのカバレッジ Toolkit の概要
ms.assetid: eead0c9a-fc26-4777-b19a-e97b898e28a2
keywords:
- ドライバーのカバレッジ Toolkit について、カバレッジ Toolkit のドライバーの WDK、
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e7262b7b1d0aaa7bc5244fb7c7d795f0dfb5f72
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537349"
---
# <a name="overview-of-the-driver-coverage-toolkit"></a>ドライバーのカバレッジ Toolkit の概要


**注**  ドライバーのカバレッジ Toolkit は Windows 10 で不要になったと、インストーラーが WDK に含まれていません。 ここで説明されている Windows 10 でタスクを実行する代わりに使用[Driver Verifier](driver-verifier.md)と[IRP のログ記録](irp-logging.md)します。

 

ドライバの対応 toolkit の監視およびレポート、I/O 要求パケット (Irp) を入力するか、1 つのドライバー スタックのままにするか、複数の指定されたデバイス。 カバレッジ データがによって収集された、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)これらのデバイス。 ドライバーのカバレッジ ツールを有効にするか、指定したデバイスは、IRP のカバレッジを無効にするだけでなくカバレッジ データからレポートを作成に使用されます。

ドライバの対応のツールキットが収集され、3 つのメトリックに基づく IRP カバレッジ データを報告します。

<span id="Major__MJ__IRP_Function_Codes"></span><span id="major__mj__irp_function_codes"></span><span id="MAJOR__MJ__IRP_FUNCTION_CODES"></span>メジャー (MJ) IRP の関数コード  
デバイスのドライバー スタック内でアクティブだった Irp の MJ 関数のコードの数。 ドライバの対応 toolkit は、12 MJ 関数コードのデータを収集します。 これらの関数コードの詳細については、次を参照してください。 [IRP の主な機能コード](https://msdn.microsoft.com/library/windows/hardware/ff550710)します。

<span id="Major__MJ__and_Minor__MN__IRP_Function_Codes"></span><span id="major__mj__and_minor__mn__irp_function_codes"></span><span id="MAJOR__MJ__AND_MINOR__MN__IRP_FUNCTION_CODES"></span>メジャー (MJ) と IRP 関数コードのマイナー (MN)  
MJ IRP の関数コードで、その下位 MN 関数コードと共に、デバイスのドライバー スタック内でアクティブだった Irp の数。 ドライバの対応 toolkit は、52 MJ および mn の各関数のコードのデータを収集します。

<span id="IRP_Pairs"></span><span id="irp_pairs"></span><span id="IRP_PAIRS"></span>IRP のペア  
デバイスのドライバー スタック内で同時にアクティブだった MJ と MJ/MN IRP の関数コードの数。 この数には、個別の Irp が入力または同時に、ドライバー スタックのままの回数が反映されます。 ドライバの対応 toolkit は、1099 MJ および mn の各関数のコードのペアのデータを収集します。

IRP の関数コードの詳細については、次を参照してください。 [IRP 関数コード](https://msdn.microsoft.com/library/windows/hardware/ff550706)します。

### <a name="span-idirpcoveragedataspanspan-idirpcoveragedataspanirp-coverage-data"></a><span id="irp_coverage_data"></span><span id="IRP_COVERAGE_DATA"></span>IRP カバレッジ データ

IRP が入るかによって監視されているデバイスのドライバー スタックを出るときに、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)、フィルター ドライバーは IRP に関連するカウンターをインクリメントします。 ドライバの対応のフィルター ドライバーは Irp が発生した方法に関係なく、ドライバー スタック内のアクティブな Irp を監視します。 その結果、フィルターは、監視ウィンドウ IRP のドライバーのフィルター ドライバーの下位のすぐに階層は、スタック内のすべてのドライバーをについて説明します。

[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md) IRP がドライバー スタック内で最初に監視する際に、その IRP カウンターをインクリメントします。 IRP がドライバー スタックの外部で行われた場合、ドライバーのカバレッジ フィルター ドライバーは IRP スタックの入力時に IRP のカウンターをインクリメントします。 フィルター ドライバーに IRP がドライバー スタック内のドライバーから発生した、IRP がドライバー スタックが離れるときにそのカウンターをインクリメントします。

次の図は、デバイスのドライバー スタック内の IRP トラフィックの例を示します。

![デバイスのドライバー スタック内の i/o 要求パケット (irp) トラフィックを示す図](images/coverage-3.png)

この例で、[ドライバー カバレッジ フィルター ドライバー](driver-coverage-filter-driver.md)次 Irp を監視します。

-   IRP A: ドライバー スタックが入力だけです。

-   IRP B: はドライバー スタックのままにします。

ドライバの対応のフィルター ドライバーは、両方の Irp の MN および MN/MJ 関数のコードのカウンターをインクリメントします。 また、A と B の両方の Irp がドライバー スタック内でアクティブなため、ドライバー カバレッジ フィルター ドライバーは {IRP A, B の IRP} のタプルの IRP のペアのカウンターをインクリメントします。

### <a name="span-idirppaircoveragedataspanspan-idirppaircoveragedataspanirp-pair-coverage-data"></a><span id="irp_pair_coverage_data"></span><span id="IRP_PAIR_COVERAGE_DATA"></span>IRP のペアでカバレッジ データ

IRP のペアでカバレッジ データは、複数の Irp のドライバー スタック内でアクティブな同時に、IRP の同時実行に基づいています。 このデータは、ドライバーの検証中に、テスト カバレッジの穴を特定するのに役立ち、ドライバーの同時実行の問題を解決するためのテストの向上に役立ちます。

ドライバの対応 toolkit モニターと 1099 MJ および mn の各関数のコードのペアに関するレポートします。

### <a name="span-idsampleirpcoveragereportspanspan-idsampleirpcoveragereportspansample-irp-coverage-report"></a><span id="sample_irp_coverage_report"></span><span id="SAMPLE_IRP_COVERAGE_REPORT"></span>IRP カバレッジ レポートのサンプル

次のコマンドには、次の例のような IRP カバレッジ レポートを作成できます。

```
Getting coverage data
 Data source
 Source Type:  Driver
 Source Name:  \\.\DrvcovControl1
 Device
   Friendly Name : USB Mass Storage Device 
   Class Name    : USB 
   Device ID     : USB\VID_04E8&PID_0100\2151151132436 
   Device #      : 1 
 Devnode #     : 5088 

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

 

 





