---
title: ERESOURCE 構造体の概要
description: ERESOURCE 構造体の概要
ms.assetid: 5c7759db-aeb5-47f3-8adc-ddedb74b5cb4
keywords:
- 次の構造体
- 排他の待機処理の WDK カーネル
- 共有の待機処理の WDK カーネル
- 排他/共有の同期の WDK カーネル
- 同期の WDK カーネル、排他/共有
- 待機処理の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a595b09b02f7d49a32cfeeb938525f186a3823b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578210"
---
# <a name="introduction-to-eresource-routines"></a>ERESOURCE 構造体の概要





システムは、取得およびその現在の状態を確認したり、次の構造を解放するルーチンを提供します。

### <a name="acquiring-and-releasing-an-eresource-structure"></a>取得と開放を次の構造体

ドライバーは、次の構造体を使用して実装する*排他/共有の同期*します。 排他/共有の同期はように動作します。

-   任意の数のスレッドは、共有として、次を取得できます。

-   1 つのスレッドでは、のみ、スケジュールの作成を取得できます。 ÷ リソースだけを専用のスレッドが既に取得がない場合、共有として取得できます。

÷ リソースを取得するまで、÷ リソースを取得できません現在のスレッドは必要に応じて待機状態で配置できます。 システムは、スケジュールの作成を待機しているスレッドの 2 つのリストを保持: 一連の*排他待機処理*の一覧と*待機処理の共有*。

排他/共有の同期の一般的な用途では、読み取り/書き込みロックを実装します。 読み取り/書き込みロックは、読み取り操作を実行する複数のスレッドが 1 つのスレッドが同時に書き込むことができます。 これは、次の取得の観点から直接実装できます。

ドライバーは、次に、記憶域を割り当てますで初期化して[ **ExInitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545317)します。 システムでは、使用中のすべてのスケジュール作成構造体のリストを保持します。 呼び出す必要がありますが、ドライバーでは、特定のスケジュール作成が必要なくなる、 [ **ExDeleteResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544578)システムの一覧から削除します。 ドライバーが、呼び出すことによって、スケジュール作成再利用できるも[ **ExReinitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545542)します。

ドライバーは、次に、次の基本的な操作を実行できます。

-   共有として、次の取得[ **ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)します。 このルーチンは、リソースが排他的に取得されていないと、排他待機処理がない場合にのみ、リソースを取得します。

-   取得のみで、スケジュール作成[ **ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)します。 取得されていないのみまたは共有のいずれかであれば、このルーチンは、リソースを取得します。

-   排他の取得をによる取得を共有する変換[ **ExConvertExclusiveToSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544558)します。

-   取得したリソースを解放[ **ExReleaseResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545597)します。

*待機*パラメーターの[ **ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363)と[ **ExAcquireResourceExclusiveLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544351)が獲得される次の現在のスレッドが待機するかどうかを決定します。 値を指定する場合**FALSE** 、÷ リソースを取得することはできませんし、ルーチンを返します**FALSE**します。 値を指定する場合**TRUE**、現在のスレッドは、次の適切な待機リストに配置します。

### <a name="examining-the-state-of-an-eresource-structure"></a>次の構造体の状態を調べる

ドライバーは、スケジュール作成の現在の状態を次のように特定もできます。

-   使用[ **ExIsResourceAcquiredLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545466)または[ **ExIsResourceAcquiredSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545477)スケジュールの作成が既にかどうかを判断するには共有または排他として取得します。 使用[ **ExIsResourceAcquiredExclusiveLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545458)かどうか、スケジュールの作成が取得されている具体的には排他的にチェックします。

-   使用して、 [ **ExGetSharedWaiterCount** ](https://msdn.microsoft.com/library/windows/hardware/ff545290) 、次の共有の待機処理の数を決定して、使用する[ **ExGetExclusiveWaiterCount** ](https://msdn.microsoft.com/library/windows/hardware/ff544618)、次の排他待機処理の数を決定します。

 

 




