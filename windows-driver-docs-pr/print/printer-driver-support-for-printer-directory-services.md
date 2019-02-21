---
title: ディレクトリ サービスのプリンターのプリンター ドライバーのサポート
description: ディレクトリ サービスのプリンターのプリンター ドライバーのサポート
ms.assetid: 6b0b3cda-a9e5-458d-b5e2-89667059bde4
keywords:
- ディレクトリ サービスの WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99a55de61a9bf2b9e77bee24b5c4ef2b0016ec90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528359"
---
# <a name="printer-driver-support-for-printer-directory-services"></a>ディレクトリ サービスのプリンターのプリンター ドライバーのサポート





プリンター ドライバーはディレクトリ サービスへの印刷キューを公開するために責任を負いません。 Microsoft Windows 2000 およびそれ以降の印刷フォルダーは、印刷キューのオブジェクトを作成します (スプーラーを呼び出すことによって**SetPrinter**関数)、プリンターのインストールの処理中にします。 (を参照してください[印刷キューを公開](print-spooler-support-for-printer-directory-services.md#ddk-publishing-print-queues-gg))。

ユーザーを使用して特定のプロパティを持つプリンターを検索できるように、印刷キューのプロパティが公開された、**検索**タスク バーの オプション**開始**メニュー。 印刷のフォルダーは、利用できることを DriverCapabilities からプリンターの機能のすべてではなく、一部を公開します。 参照のための便利なと見なされる機能のみが発行されます。

プリンター ドライバーでは、追加したり、印刷キュー オブジェクトのプロパティ情報を変更することができます。 パブリッシュできる印刷キューのプロパティがで識別される**SPLDS\_**-winspool.h で定義されている定数の先頭します。 を追加またはプリンターのプロパティを変更するには、ドライバーはこれらの定義済みのプロパティ名の識別子を使用する必要があります。

を追加または印刷キュー オブジェクトのプロパティ情報を変更するには、次の手順を実行します。

1.  プロパティの名前と値を SPLDS の下のレジストリに追加\_ドライバー\_スプーラーを呼び出すことによって、キー **SetPrinterDataEx**関数。

2.  呼び出す、スプーラーの**SetPrinter**関数は、プリンターの入力の構造を持つ\_情報\_7 (Windows SDK のドキュメントで説明) と DSPRINT のアクション\_スプーラーを通知するために、更新プログラムその it では、パブリッシュされた印刷キューのオブジェクトを更新する必要があります。 (ドライバー DSPRINT のアクションを指定しないでください\_発行します)。

次の手順は、プリンター ドライバーの内で実装する必要があります[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)関数、関数は、プリンターを受信すると\_イベント\_INITIALIZE イベント。

呼び出す必要がありますが、ドライバーは、プリンターのプロパティの発行済みの現在の値を取得する必要がある場合、 **GetPrinterDataEx**または**EnumPrinterDataEx**はレジストリから情報を取得するにはスプーラで維持されると常に最新の状態。 呼び出す別の方法は、 **GetPrinter**印刷キューのオブジェクト識別子を取得し、公開されたプロパティの値を取得する ADSI 関数を呼び出します。 この手法は推奨されませんより多くのリソース集中型であるとデータが必ずしも現在返されるためです。

 

 




