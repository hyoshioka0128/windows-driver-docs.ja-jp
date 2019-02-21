---
title: オプション ファイル フィールド
description: オプション ファイル フィールド
ms.assetid: 5ca79c91-5d19-4393-aa5e-be3d47e62967
keywords:
- ファイル WDK Static Driver Verifier のオプション
- WDK Static Driver Verifier のフィールド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 045168ae1a1e38d8a591937e6ef66aa45aa0aedb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552240"
---
# <a name="option-file-fields"></a>オプション ファイル フィールド


SDV のオプションをファイルには、SDV 設定が含まれています。 いくつかのこれらの設定を変更することができます。 その他の設定は、SDV で予約されています。

変更可能なオプションのファイルのフィールドを以下に示します。

<span id="SDV_SlamConfig_Maximum_Driver_Size"></span><span id="sdv_slamconfig_maximum_driver_size"></span><span id="SDV_SLAMCONFIG_MAXIMUM_DRIVER_SIZE"></span>**SDV\_SlamConfig\_最大\_ドライバー\_サイズ**  
SDV は、(行のコード) の観点からサポートするドライバーの最大サイズを指定します。 既定値は、100 K 行のコードです。

<span id="SDV_SlamConfig_Timeout"></span><span id="sdv_slamconfig_timeout"></span><span id="SDV_SLAMCONFIG_TIMEOUT"></span>**SDV\_SlamConfig\_タイムアウト**  
SDV は各ルールの検証に費やす時間を制限します。 このエントリの値は、秒数を表す整数です。 最小値は 10、最大値は 86400、および既定値は 3000 (50 分)。

SDV は、ルールの確認中にルールごとに時間制限を超えている場合、検証とレポート終了、**タイムアウト**で、[コマンドライン出力](command-line-output.md)と [結果] セクションで Static Driver Verifier**Main**タブ。

<span id="SDV_SlamConfig_Spaceout"></span><span id="sdv_slamconfig_spaceout"></span><span id="SDV_SLAMCONFIG_SPACEOUT"></span>**SDV\_SlamConfig\_Spaceout**  
SDV は各ルールを検証するときに使用できる仮想メモリの量を制限します。 このエントリの値は、メガバイト (MB) 単位の整数です。 最小値は 100、および既定値は、2500 MB (2.5 GB)。

SDV は、ルールの確認中に、仮想メモリ制限を超えている場合、検証とレポート終了、 **Spaceout**で、[コマンドライン出力](command-line-output.md)と [結果] セクションの Static Driver Verifier**Main**タブ。

SDV の報告された場合、 **Spaceout**の値を増やすことを検討**SDV\_SlamConfig\_Spaceout**SDV を実行している場合、または移動中に、コンピューター上の他のすべてのプロセスを停止しています多くのメモリを使用してコンピューターに SDV します。 システムの最適な値は、約 200 MB 未満のシステム上の物理メモリの量です。

<span id="SDV_SlamConfig_NumberOfThreads"></span><span id="sdv_slamconfig_numberofthreads"></span><span id="SDV_SLAMCONFIG_NUMBEROFTHREADS"></span>**SDV\_SlamConfig\_NumberOfThreads**  
検証中に使用するスレッドの数を設定します。 値が 0 の場合は、この (ハイパー スレッド プロセッサを含む)、コンピューター上のプロセッサの数のスレッドの数を制限します。 値を 0 より大きい数値を設定すると、値は、SDV は、検証中に使用できるスレッドの数を指定します。 SDV の実行時のパフォーマンスを向上させる可能性がありますスレッドの数を増やすことは、発生したタイムアウトの数も改善可能性があります。 既定値は 0 です。 SDV を既定値を使用するマルチプロセッサ コンピューターで実行する場合は、SDV は、さらにプロセッサを利用自動的に。

 

 





