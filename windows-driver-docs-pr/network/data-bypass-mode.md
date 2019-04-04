---
title: データ バイパス モード
description: データ バイパス モード
ms.assetid: 98061803-22de-4fa2-8582-2d382f84dd75
keywords:
- フィルター ドライバー WDK ネットワーク、データのバイパス モード
- NDIS フィルター ドライバー WDK、データのバイパス モード
- データは、モード WDK ネットワークをバイパスします。
- バイパス モード WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cbc5a083d7f67f3083cb66eb1c1172328350023
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572229"
---
# <a name="data-bypass-mode"></a>データ バイパス モード





フィルター ドライバー*データ バイパス モード*システム パフォーマンスの向上を提供することができます。 NDIS は呼び出しません*FilterXxx*関数がバイパスされます。 たとえば場合、送信および受信サービスではありません。 指定したフィルター アプリケーションに必要なフィルター ドライバーは、送信をバイパスでき、受信機能。

フィルター ドライバーが関数を呼び出すときに、ドライバーの初期化中に、省略可能で、既定のエントリ ポイントを指定します、 [ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)関数。 エントリ ポイントは、 **NULL**関数で、既定では省略されます。 初期化の詳細については、[フィルター ドライバーの初期化](initializing-a-filter-driver.md)を参照してください。

実行時にバイパスの状態を変更するには、ドライバーがのエントリ ポイントを指定する必要があります、 [ *FilterSetModuleOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549970)ドライバーの初期化中に機能します。 ドライバーを初期化できます、 [ **NDIS\_フィルター\_部分\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565544)構造体し、する新しい特性を渡す、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)のコンテキスト内で関数を*FilterSetModuleOptions*します。

NDIS 呼び出し、 *FilterSetModuleOptions*関数は、再起動操作の開始時に存在します。 フィルター ドライバーは、各フィルター モジュールを個別にバイパス モードを設定できます。 詳細については、[フィルター モジュールの開始](starting-a-filter-module.md)を参照してください。

フィルター ドライバーは、次のオプションをバイパスできる*FilterXxx*関数で指定されている、 [ **NDIS\_フィルター\_ドライバー\_の特性**](https://msdn.microsoft.com/library/windows/hardware/ff565515)構造体。

[*FilterSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549966)

[*FilterSendNetBufferListsComplete*](https://msdn.microsoft.com/library/windows/hardware/ff549967)

[*FilterCancelSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549915)

[*FilterReturnNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549964)

[*FilterReceiveNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549960)

設定する、 *FilterXxx*フィルター ドライバーを指定します、モードをバイパスする関数**NULL**関数のエントリ ポイント。 ただし、ドライバーが任意の NDIS 関数を呼び出す場合ですが、関連付けられている*FilterXxx*関数の場合、そのエントリ ポイントを提供する必要があります*FilterXxx*関数。 ドライバーを呼び出す場合など、 [ **NdisFIndicateReceiveNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff561820)関数を提供する必要がありますが、 [ *FilterReturnNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549964)関数。

フィルター ドライバーが指定されている場合、 [ *FilterSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549966)関数を送信要求をキューに配置する必要がありますも指定する必要が、 [ *FilterCancelSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff549915)関数。

フィルター ドライバーが指定されている場合、 [ *FilterReceiveNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff549960)または[ **FilterReturnNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff549964)関数の場合、ドライバーの必要があります指定することも、 [ *FilterStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff549973)関数。

実行時にバイパス モード設定を変更、フィルター ドライバーを呼び出すことができます、 [ **NdisFRestartFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff562611)関数。 **NdisFRestartFilter**が指定されたフィルター モジュールの再起動操作している操作を一時停止をスケジュールします。 NDIS を呼び出すと*FilterSetModuleOptions*、フィルター ドライバーはそのフィルター モジュールの関数を呼び出すことで変更できる**NdisSetOptionalHandlers**エントリ ポイントの新しいセットを指定するとします。

**注**  一時停止と再起動、送信パス上にドロップするいくつかのネットワーク パケット、またはパス、またはその両方を受信します。 信頼性の高いトランスポート メカニズムを提供するネットワーク プロトコルがネットワークの場合は、損失パケットを I/O 操作を再試行可能性がありますが、信頼性を保証しないその他のプロトコルは、操作を再試行しないでください。

 

フィルター ドライバーは、オプションのドライバー サービスをサポートする追加の省略可能な関数を登録できます。 ドライバーはこれらの省略可能なサービスに登録、 [ *FilterSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549972)関数。 これらの省略可能なサービスに関する詳細については、[省略可能なフィルター ドライバー サービスを構成する](configuring-optional-filter-driver-services.md)を参照してください。

 

 





