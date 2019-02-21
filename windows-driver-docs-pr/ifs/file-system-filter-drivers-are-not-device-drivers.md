---
title: ファイル システム フィルター ドライバーは、デバイス ドライバーではありません。
description: ファイル システム フィルター ドライバーは、デバイス ドライバーではありません。
ms.assetid: 4a1b2470-0062-4241-952d-ea9351b1a2f9
keywords:
- フィルター ドライバー WDK ファイル システム、デバイス ドライバーとの比較
- ファイル システム フィルター ドライバー WDK、デバイス ドライバーとの比較
- デバイス ドライバー WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a2c42aa75aa10d6ccd743c512ab54219e4a69e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531323"
---
# <a name="file-system-filter-drivers-are-not-device-drivers"></a>ファイル システム フィルター ドライバーは、デバイス ドライバーではありません。


## <span id="ddk_a_file_system_filter_driver_is_not_a_device_driver_if"></span><span id="DDK_A_FILE_SYSTEM_FILTER_DRIVER_IS_NOT_A_DEVICE_DRIVER_IF"></span>


A*デバイス ドライバー*は特定のハードウェア I/O デバイスを制御するソフトウェア コンポーネントです。 たとえば、DVD の記憶装置ドライバーは、DVD ドライブを制御します。

これに対し、ファイル システム フィルター ドライバーは、ファイル I/O 操作を管理する 1 つまたは複数のファイル システムと組み合わせて動作します。 これらの操作には、作成、開く、閉じる、およびファイルおよびディレクトリの列挙が含まれます。ファイル、ディレクトリ、およびボリューム情報の取得および設定読み取りとファイル データの書き込み。 さらに、ファイル システム フィルター ドライバーする必要がありますロックをサポートなど、キャッシュ、ファイル システムに固有の機能、スパース ファイル、ディスク クォータ、圧縮、セキュリティ、回復性、再解析ポイント、およびボリューム マウント ポイント。

ファイル システム フィルター ドライバーとデバイス ドライバーの間の相違点の詳細については、次を参照してください。

[ファイル システム フィルター ドライバーのデバイス ドライバーのような方法](how-file-system-filter-drivers-are-similar-to-device-drivers.md)

[ファイル システム フィルター ドライバーのデバイス ドライバーからさまざまな方法](how-file-system-filter-drivers-are-different-from-device-drivers.md)

 

 




