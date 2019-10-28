---
title: 移植できるドライバーと場所
description: このトピックでは、Windows ドライバーフレームワーク (WDF) に移植できる WDM ドライバーと、カーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) のどちらに移植するかを決定する方法について説明します。
ms.assetid: 53E34B9C-8C0A-4F15-951B-7AB133DE0C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e85cdca164a1ee217e38ada5fe286620715a104
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842788"
---
# <a name="which-drivers-can-be-ported-and-where"></a>移植できるドライバーと場所


このトピックでは、Windows ドライバーフレームワーク (WDF) に移植できる WDM ドライバーと、カーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) のどちらに移植するかを決定する方法について説明します。

## <a name="which-wdm-drivers-can-i-port-to-wdf"></a>どの WDM ドライバーを WDF に移植できますか。


特定のドライバーを WDF に移植できるかどうかは、次の条件によって異なります。

-   ドライバーが実行されているオペレーティングシステムのバージョン
-   ドライバーがサポートするデバイスの種類
-   ドライバーが使用するドライバーモデル

一般に、KMDF または UMDF を使用して、WDM に準拠したドライバーを記述し、主要な i/o ディスパッチルーチンのエントリポイントを指定し、Irp を処理できます。

デバイスの種類によっては、システムによって提供されるデバイスクラスとポートドライバーによってドライバーディスパッチ関数が提供され、ベンダーが提供するミニポートドライバーを呼び出して特定の i/o の詳細を処理します。 これらのミニポートドライバーは基本的にコールバックライブラリであり、WDF ではサポートされていません。 また、WDF は、Windows イメージ取得 (WIA) を使用するデバイスの種類をサポートしていません。

KMDF を使用して、Windows 2000 以降で実行されるドライバーを作成できます。 UMDF version 1 を使用して、Windows XP 以降で実行されるドライバー、および Windows 8.1 以降を対象とする UMDF version 2 を作成できます。

UMDF および KMDF がサポートするデバイスとドライバーの種類の詳細については、「[ドライバーモデルの選択](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)」を参照してください。

## <a name="which-framework-should-i-port-my-wdm-driver-to-kmdf-or-umdf-2"></a>WDM ドライバーを KMDF または UMDF 2 に移植する必要があるのはどのフレームワークですか。


1.  [UMDF 2.0 機能と KMDF の比較](comparing-umdf-2-0-functionality-to-kmdf.md)に関する kmdf のみの機能の一覧を確認します。 ドライバーがこれらの機能のいずれも必要とせず、Windows 8.1 以降を対象としている場合は、Visual Studio で新しい UMDF 2 ドライバーテンプレートを開きます。

    後で KMDF のみの機能が必要になった場合は、「 [KMDF ドライバーを umdf 2.0 ドライバーに変換する方法 (およびその逆)](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)」で説明されているように、umdf 2 ドライバーを kmdf に変換するのは簡単です。

2.  また、*モードに依存*しないドライバー (kmdf または UMDF を使用してコンパイルできるドライバー) を記述することもできます。 モードに依存しないドライバーを作成するには、まず、UMDF 2 テンプレートを使用します。 「 [WDF コールバックとメソッドの概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)」に記載されている DDI のバージョン管理情報を使用して、KMDF と UMDF 2 の両方で使用可能なメソッドのみを呼び出すようにします。 「 [KMDF ドライバーを UMDF 2.0 ドライバーに変換する方法 (およびその逆)](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)」で説明されているプリプロセッサマクロを使用して、任意のヘッダー参照にタグ付けします。 ドライバーを切り替えるには、ターゲットフレームワーク用の Visual Studio テンプレートを使用して空のドライバープロジェクトを作成し、ソースコードをにコピーします。

## <a name="related-topics"></a>関連トピック


[UMDF の概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)

[KMDF のバージョン履歴](kmdf-version-history.md)

[UMDF バージョン履歴](umdf-version-history.md)

[ユーザーモードドライバーフレームワークに関してよく寄せられる質問](user-mode-driver-framework-frequently-asked-questions.md)

 

 






