---
title: ファイル システム フィルター ドライバーについて
description: ファイル システム フィルター ドライバーについて
ms.assetid: 4bff8ad6-624a-429d-b9ec-3f96c3c7c99d
keywords:
- フィルタードライバー WDK ファイルシステム、ファイルシステムフィルタードライバーについて
- ファイルシステムフィルタードライバー WDK、ファイルシステムフィルタードライバーについて
- ファイルシステムフィルタードライバーとは
- ファイルシステムフィルタードライバーはデバイスドライバーではありません
ms.date: 02/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 61d74ef606eda5f0acfa25018f7bdf92edc201b4
ms.sourcegitcommit: 677a9aeb3fb0c29fd8984f271fd803f15182fdb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80226530"
---
# <a name="about-file-system-filter-drivers"></a>ファイル システム フィルター ドライバーについて

## <a name="file-system-filter-drivers-on-windows"></a>Windows 上のファイルシステムフィルタードライバー

*ファイルシステムフィルタードライバー*は、ファイルシステムの動作に値を追加したり、ファイルシステムの動作を変更したりするためのオプションのドライバーです。 ファイルシステムフィルタードライバーは、Windows executive の一部として実行されるカーネルモードのコンポーネントです。

ファイルシステムフィルタードライバーは、1つまたは複数のファイルシステムまたはファイルシステムボリュームの i/o 操作をフィルター処理できます。 *フィルター*は、ドライバーの性質によっては、*ログ記録*、*監視*、*変更*、または*回避*することを意味します。 ファイルシステムフィルタードライバーの一般的なアプリケーションには、ウイルス対策ユーティリティ、暗号化プログラム、階層型記憶域管理システムなどがあります。

Windows には、次の2つのファイルシステムフィルターモデルがあります。

- ミニフィルター[モデル](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)。ミニフィルターでは、システムによって提供されるフィルターマネージャーサポートを使用します。これにより、フィルターの開発が簡素化されます。

- [レガシファイルシステムフィルターモデル](https://docs.microsoft.com/windows-hardware/drivers/ifs/about-file-system-legacy-filter-drivers)

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。

## <a name="file-system-filter-drivers-are-not-device-drivers"></a>ファイルシステムフィルタードライバーはデバイスドライバーではありません

*デバイスドライバー*は、特定のハードウェア i/o デバイスを制御するソフトウェアコンポーネントです。 たとえば、dvd 記憶装置ドライバーは DVD ドライブを制御します。

これに対し、ファイル*システムフィルタードライバー*は、1つまたは複数のファイルシステムと連携して、ファイル i/o 操作を管理します。 これに該当する操作は次のとおりです。

- ファイルとディレクトリの作成、開始、終了、および列挙

- ファイル、ディレクトリ、およびボリュームの情報の取得と設定

- ファイルデータの読み取りと書き込み

また、ファイルシステムフィルタードライバーは、キャッシュ、ロック、スパースファイル、ディスククォータ、圧縮、セキュリティ、回復性、再解析ポイント、ボリュームマウントポイントなどのファイルシステム固有の機能をサポートしている必要があります。

ファイルシステムフィルタードライバーとデバイスドライバーの類似点と相違点の詳細については、次を参照してください。

- [ファイルシステムフィルタードライバーとデバイスドライバーの類似点](how-file-system-filter-drivers-are-similar-to-device-drivers.md)

- [ファイルシステムフィルタードライバーとデバイスドライバーの違い](how-file-system-filter-drivers-are-different-from-device-drivers.md)
