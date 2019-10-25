---
title: プリンタードライバーでのプリンターディレクトリサービスのサポート
description: プリンタードライバーでのプリンターディレクトリサービスのサポート
ms.assetid: 6b0b3cda-a9e5-458d-b5e2-89667059bde4
keywords:
- ディレクトリサービス WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb957dc2089b39c0c3778cbdf946aa12900abb68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840433"
---
# <a name="printer-driver-support-for-printer-directory-services"></a>プリンタードライバーでのプリンターディレクトリサービスのサポート





プリンタードライバーは、印刷キューをディレクトリサービスに発行する役割を持ちません。 Microsoft Windows 2000 以降の印刷フォルダーは、プリンターのインストール処理中に (スプーラの**Setprinter**関数を呼び出すことによって) 印刷キューオブジェクトを作成します。 ([印刷キューの発行](print-spooler-support-for-printer-directory-services.md#ddk-publishing-print-queues-gg)に関するページを参照してください)。

印刷キューのプロパティは、ユーザーがタスクバーの **[スタート]** メニューの **[検索]** オプションを使用して、特定のプロパティを持つプリンターを検索できるように公開されます。 印刷フォルダは、ドライバ機能から使用できるプリンタ機能の一部を公開しますが、すべてではありません。 参照のために役に立つと思われる機能のみが公開されています。

プリンタードライバーは、印刷キューオブジェクトのプロパティ情報を追加または変更できます。 発行できる印刷キューのプロパティは、winspool で定義されている、 **\_** プレフィックス付き定数によって識別されます。 プリンターのプロパティを追加または変更するには、ドライバーでこれらの定義済みプロパティ名識別子を使用する必要があります。

印刷キューオブジェクトのプロパティ情報を追加または変更するには、次の手順を実行します。

1.  スプーラの**Setプリンター Dataex**関数を呼び出して、プロパティの名前と値をレジストリの\_ドライバー\_キーの下に追加します。

2.  スプーラーに、発行された印刷を更新する必要があることをスプーラに通知するには、PRINTER\_INFO\_7 (Windows SDK のドキュメントで説明) という入力構造と DSPRINT\_UPDATE のアクションを使用して、スプーラの**Setprinter**関数を呼び出します。queue オブジェクト。 (ドライバーは、\_発行の DSPRINT のアクションを指定することはできません)。

これらの手順は、プリンタードライバーの[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)関数内に実装する必要があります。これは、関数がプリンター\_イベント\_INITIALIZE イベントを受信したときに実行されます。

ドライバーがプリンターの公開されたプロパティの現在の値を取得する必要がある場合は、 **Getprinter dataex**または**Enumprinter dataex**を呼び出して、レジストリから情報を取得する必要があります。この情報は、スプーラによって保持され、常に最新の状態にあります。 別の方法として、 **Getprinter**を呼び出して印刷キューのオブジェクト識別子を取得し、次に ADSI 関数を呼び出して、公開されているプロパティの値を取得します。 この手法は、リソースを大量に消費し、返されるデータが常に最新であるとは限りません。そのため、この方法はお勧めしません。

 

 




