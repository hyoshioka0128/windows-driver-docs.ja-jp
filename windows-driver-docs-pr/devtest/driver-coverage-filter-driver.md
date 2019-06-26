---
title: Driver Coverage フィルター ドライバー
description: Driver Coverage フィルター ドライバー
ms.assetid: 8d345081-b9be-4e22-9276-dacd7815f506
keywords:
- ドライバーのカバレッジ Toolkit WDK、フィルター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 678682048e05d246d8a19c1370eefeacd65f515e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360355"
---
# <a name="driver-coverage-filter-driver"></a>Driver Coverage フィルター ドライバー


**注**  ドライバーのカバレッジ Toolkit は Windows 10 で不要になったと、インストーラーが WDK に含まれていません。 ここで説明されている Windows 10 でタスクを実行する代わりに使用[Driver Verifier](driver-verifier.md)と[IRP のログ記録](irp-logging.md)します。

 

ドライバーのカバレッジ フィルター ドライバー (Drvcov.sys) を入力するか、指定されたデバイスのドライバー スタックのままにする I/O 要求パケット (Irp) を監視します。 使用して、ドライバの対応フィルター ドライバーを監視するデバイスを指定する、 *DQ*パラメーターを実行すると、 **IRP のカバレッジを有効にするデータ コレクション**ツール。 参照してください[を選択して、デバイスの基本テストを構成する方法](https://docs.microsoft.com/windows-hardware/drivers)と[デバイス基礎テスト パラメーター](https://docs.microsoft.com/windows-hardware/drivers)します。

<span id="UpperFilter___TRUE"></span><span id="upperfilter___true"></span><span id="UPPERFILTER___TRUE"></span>**UpperFilter = TRUE**  
このオプションは、デバイス ドライバーを指定されたデバイスの上部のフィルターとして、ドライバーのカバレッジ フィルター ドライバーをインストールします。 この構成は、ドライバーが IRP の処理または下位のデバイス ドライバーにを通じて渡されるかどうかに関係なく、デバイスのドライバー スタック内のデバイス ドライバーの内外に IRP のすべてのトラフィックを監視します。

<span id="UpperFilter___FALSE"></span><span id="upperfilter___false"></span><span id="UPPERFILTER___FALSE"></span>**UpperFilter = FALSE**  
このオプションは、指定したデバイスのデバイス ドライバーに下位のフィルターとして、ドライバーのカバレッジ フィルター ドライバーをインストールします。 この構成は、デバイスのドライバー スタック内の下位のドライバーからデバイス ドライバーの内外に IRP のすべてのトラフィックを監視します。

次の図は、スタック、IRP 監視デバイスのウィンドウ上部のフィルターとして、ドライバーのカバレッジ フィルター ドライバーがインストールされているドライバーを示します。 この構成では、フィルター ドライバーは、入力するか、指定されたデバイス ドライバーのままにするすべての Irp を追跡します。

![上部のフィルターとしてインストールされたドライバー カバレッジ フィルター ドライバーを示す図](images/coverage-1.png)

次の図は、スタック、IRP 監視デバイスのウィンドウ下部のフィルターとして、ドライバーのカバレッジ フィルター ドライバーがインストールされているドライバーを示します。 この構成では、フィルター ドライバーは、入力するか、指定されたデバイスのドライバー スタックは、デバイス ドライバーのままにするすべての Irp を追跡します。

![下位のフィルターとしてインストールされたドライバー カバレッジ フィルター ドライバーを示す図](images/coverage-2.png)

.

### <a name="span-idinstallingthedrivercoveragefilterdriverspanspan-idinstallingthedrivercoveragefilterdriverspan-installing-the-driver-coverage-filter-driver"></a><span id="installing_the_driver_coverage_filter_driver"></span><span id="INSTALLING_THE_DRIVER_COVERAGE_FILTER_DRIVER"></span> ドライバの対応のフィルター ドライバーをインストールします。

次の規則は Irp を監視するドライバの対応のフィルター ドライバーをインストールする最善の方法を定義します。

-   カバレッジ データ IRP トラフィック特定のデバイスとユーザー モード アプリケーションまたはサービスの間に必要な場合は、デバイスのドライバーに上位のフィルターとして、フィルター ドライバーをインストールします。

-   場合カバレッジ データ、指定されたデバイスとデバイス間のトラフィックの IRP のデバイスの場合、バス ドライバーなど、ドライバー スタックの下位インストール フィルター ドライバー、デバイスのドライバーに下位のフィルターとして。

**注**  ドライバー カバレッジ フィルター ドライバーをインストールする方法の IRP の最適なカバレッジがドライバー スタックのトポロジに依存し、リレーションシップと、ドライバー、スタック内の順序を理解することが必要です。

 

 

 





