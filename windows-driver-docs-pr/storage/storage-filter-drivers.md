---
title: 記憶域フィルター ドライバー
description: 記憶域フィルター ドライバー
ms.assetid: 615e8ff1-d5b2-49da-b024-83bbaff70ded
keywords:
- 記憶域フィルター ドライバー WDK
- フィルター ドライバー WDK ストレージ
- ストレージ ドライバー WDK、フィルター ドライバー
- SFD WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2600d7b828c92d48b2a05431ae2f62d4ecfc8c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539706"
---
# <a name="storage-filter-drivers"></a>記憶域フィルター ドライバー


## <span id="ddk_storage_filter_drivers_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_KG"></span>


このセクションには、次の情報が含まれています。

[I/O 要求の記憶域フィルター ドライバーのサポート](storage-filter-driver-s-support-of-i-o-requests.md)

[記憶域フィルター ドライバーのデバイスの種類に固有の機能](storage-filter-driver-s-device-type-specific-functionality.md)

[記憶域フィルター ドライバーの DriverEntry ルーチン](storage-filter-driver-s-driverentry-routine.md)

[記憶域フィルター ドライバー AddDevice ルーチン](storage-filter-driver-s-adddevice-routine.md)

[ストレージのフィルター ドライバーの PnP 開始の処理](handling-pnp-start-in-a-storage-filter-driver.md)

[記憶域フィルター ドライバーのディスパッチ ルーチン](storage-filter-driver-s-dispatch-routines.md)

[記憶域フィルター ドライバーの IoCompletion ルーチン](storage-filter-driver-s-iocompletion-routines.md)

[PnP ページング要求の処理](handling-pnp-paging-requests.md)

デバイスの特定の種類のストレージ クラス ドライバーが既に存在する場合が同じ型の新しいデバイスのドライバーを記述するために必要なできない可能性があります。 各システムが指定したストレージ クラス ドライバーは、指定された型の周辺機器をサポートするために設計されていてがさまざまなベンダーのデバイスに対してテストします。 したがって、任意のシステムが指定したストレージ クラス ドライバー可能性がありますすべてサポートが提供、その型のニーズの別のデバイス。

既存の記憶域クラス ドライバーがその型の新しいデバイスが完全にサポートしない場合、または既存のシステム指定のクラス ドライバー 階層型記憶域フィルター ドライバー (SFD) として新しいドライバーを記述できます。 データを変換する場合があります、SFD、読み取り/書き込み要求を特定のデバイスの追加機能を利用したり、必要とせずにデバイスに固有の問題を回避するには、ユーザー アプリケーションを有効にする追加の I/O 制御コード (Ioctl) を定義します。ハードウェアに固有では、ジェネリック クラスまたはポート ドライバーに変更します。

新しいデバイスでは、デバイス固有の方法ですべての要求を処理することが必要なストレージのフィルター ドライバーは新しい記憶域クラス ドライバーよりもはるかに短時間で開発できます。

 

 




