---
title: 移植できるドライバーと場所
description: このトピックでは、どの WDM ドライバーは、Windows Driver Frameworks (WDF) に移植でき、カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) に移植するかどうかを決定する方法について説明します。
ms.assetid: 53E34B9C-8C0A-4F15-951B-7AB133DE0C5A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9e09e9fbe03d38f2dd0151708caba42a796e4ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376172"
---
# <a name="which-drivers-can-be-ported-and-where"></a>移植できるドライバーと場所


このトピックでは、どの WDM ドライバーは、Windows Driver Frameworks (WDF) に移植でき、カーネル モード ドライバー フレームワーク (KMDF) またはユーザー モード ドライバー フレームワーク (UMDF) に移植するかどうかを決定する方法について説明します。

## <a name="which-wdm-drivers-can-i-port-to-wdf"></a>WDF には、どの WDM ドライバーはポートでしょうか。


特定のドライバーを WDF に移植するかどうかは、次の条件によって異なります。

-   ドライバーが実行されているオペレーティング システムのバージョン
-   ドライバーがサポートするデバイスの種類
-   ドライバーを使用するドライバー モデル

一般に、ことができますを使用して KMDF または UMDF WDM に準拠している書き込みドライバーに、主要な I/O のエントリ ポイントをサプライ ディスパッチ ルーチン、Irp を処理します。

デバイスの種類によっては、システム提供のデバイス クラス、およびポートのドライバーがドライバーのディスパッチ関数を提供し、I/O の詳細を処理するためにベンダーから提供されたミニポート ドライバーを呼び出します。 これらのミニポート ドライバー コールバック ライブラリでは基本的には、WDF でサポートされていません。 また、WDF は Windows Image Acquisition (WIA) を使用して、デバイスの種類をサポートしていません。

KMDF を使用して、Windows 2000 以降を実行しているドライバーを作成することができます。 ターゲットの Windows 8.1 以降には、UMDF バージョン 1 と後で、Windows XP で実行されるドライバーを作成および UMDF バージョン 2 を使用できます。

UMDF および KMDF をサポートするデバイスとドライバーの種類については、次を参照してください。[ドライバー モデルを選択する](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/choosing-a-driver-model)します。

## <a name="which-framework-should-i-port-my-wdm-driver-to-kmdf-or-umdf-2"></a>どのフレームワーク、KMDF または UMDF 2 には、WDM ドライバーを移植する必要がありますか。


1.  KMDF 専用の機能の一覧を確認して[KMDF に UMDF 2.0 機能を比較する](comparing-umdf-2-0-functionality-to-kmdf.md)します。 ドライバーが必要としない場合、これらのいずれかの機能と、Windows 8.1 を対象とするか、後で、Visual Studio で新しい 2 の UMDF ドライバー テンプレートを開きます。

    後で、KMDF 専用の機能が必要があること認識、ある KMDF、するには、2 の UMDF ドライバーを変換する簡単な」の説明に従って[KMDF ドライバーを 2.0 の UMDF ドライバー (およびその逆) に変換する方法について](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)します。

2.  記述することも、*モードに依存しない*ドライバー、つまり、KMDF または UMDF を使用してコンパイルすることができます。 モードに依存しないドライバーを作成するには、UMDF 2 テンプレートを使用して起動します。 記載 DDI バージョン管理情報を使用して[WDF のコールバックの概要とメソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)のみ KMDF と UMDF 2 の両方で使用できるメソッドを呼び出すことを確認します。 条件付きでヘッダーの参照をタグで説明するプリプロセッサ マクロを[KMDF ドライバーを 2.0 の UMDF ドライバー (およびその逆) に変換する方法について](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)します。 ドライバーには、ターゲット フレームワークでは、Visual Studio テンプレートを使用して、空のドライバーのプロジェクトを作成し、経由で、ソース コードをコピーします。

## <a name="related-topics"></a>関連トピック


[UMDF の概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)

[KMDF バージョン履歴](kmdf-version-history.md)

[UMDF バージョン履歴](umdf-version-history.md)

[ユーザー モード ドライバー フレームワークについてよく寄せられる質問](user-mode-driver-framework-frequently-asked-questions.md)

 

 






