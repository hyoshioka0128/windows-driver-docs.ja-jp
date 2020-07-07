---
title: WIA スキャナーツリー
description: WIA スキャナーツリーは、カメラとスキャナーの両方に共通するプロパティで構成されるルート項目 (スキャナー) と各子項目に関する情報を提供します。
ms.assetid: bd1452b9-1926-4dd6-b94c-e44f07573266
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 19227961f3fa69808d3a27e42300946906e4b845
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020083"
---
# <a name="wia-scanner-tree"></a>WIA スキャナーツリー

次の図は、スキャナーとそれが生成したイメージを示しています。

![スキャナーとそれが生成したイメージを示す図](images/art-scanner.png)

次の図は、Microsoft Windows Me または Windows XP スキャナー、またはスキャナーにドキュメントフィーダー、両面印刷用スキャナーがない場合の windows Vista のスキャナーを示しています。

次の図に示すように、WIA は、前の図で示されているスキャナーとそのイメージを項目ツリーとして表します。

![wia がスキャナーとそのイメージを項目ツリーとして表す方法を示す図](images/art-4.png)

スキャナー自体であるルート項目は、一般的なデバイスプロパティ (カメラとスキャナーの両方に共通のプロパティ) とスキャナー固有のデバイスプロパティで構成されています。 同様に、各子項目は、カメラとスキャナーの両方の項目に共通するプロパティだけでなく、スキャナー項目に固有のプロパティで構成されます。

アプリケーションでは、WIA サービスを使用して、次の項目をスキャナー項目から要求できます。

- クエリスキャナーの機能

- スキャナーデバイスのプロパティを設定する

- データ転送を要求する

Windows Me と Windows XP では、ルート項目のすぐ下に、一般的なスキャナーオブジェクトには、デバイスのデータ収集機能を表すスキャナー項目という1つの項目があります。 アプリケーションは、スキャナー項目のプロパティを設定することによって、スキャンを設定します。 スキャンは、アプリケーションが、WIA サービスを介して項目からデータを要求したときに実行されます。

Windows Me と Windows XP では、通常、アプリケーションは、2つの項目 (ルート項目と1つの子) で表されるように、自動ドキュメントフィーダー (ADFs) を備えたスキャナーなどのフラットベッドスキャナーを必要とします。 すべてのデータ転送は、子項目から実行されます。 ドライバーは、プライベートに使用するために他の項目を作成することができます。これらの項目は、転送可能にすることができます。 (これを行うには、 [**wiasCreateChildAppItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem)への呼び出しで item type フラグの WiaItemTypeTransfer ビットを設定します。 この定数については、Microsoft Windows SDK のドキュメントを参照してください)。ただし、通常、アプリケーションはこれらのプライベート項目を認識しないため、それらを操作する方法がわかりません。 ADF を使用したスキャナーの場合、Windows Me または Windows XP では、スキャナーの \_ \_ \_ 子項目ではなく、WIA DPS ドキュメント処理 \_ *XXX*プロパティをスキャナーのルート項目に追加することにより、adf 機能が公開および制御されます。 これらのプロパティの詳細については、「 [WIA のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties)」を参照してください。 Windows Vista の ADF を使用したスキャナーの詳細については、「 [WIA フィーダースキャナー](wia-feeder-scanners.md)」を参照してください。

デバイスにフラットベッドおよび ADF が搭載されていて、Windows Me または Windows XP で双方向スキャンを実行できる場合、ドライバーは[**WIA \_ DPS \_ ドキュメント \_ 処理 \_ 機能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)のプロパティをとして報告します (フィード &#x7c; フラット &#x7c; DUP)。

[**WIA \_ DPS \_ ドキュメント \_ 処理の \_ 選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)の有効な値が正しく設定されていることを確認します。 1つのスキャンジョブでスキャンされたすべてのドキュメントが、項目ツリーの単一の子項目に存在することに注意してください。 ADF を備えたスキャナーと Windows Vista の両面印刷装置の詳細については、「 [WIA フィーダースキャナー](wia-feeder-scanners.md)」を参照してください。

たとえば、アプリケーションが ADF から3ページの両面スキャンを実行するとします。 これを実現するために、アプリケーションでは、WIA \_ dps \_ ドキュメント \_ 処理の \_ 選択プロパティを (フィーダー &#x7c; 双方向) に設定し、[ [**wia \_ dps \_ ページ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)] プロパティを3に設定します。 アプリケーションで最初にページの先頭をスキャンする場合は、WIA \_ DPS \_ ドキュメント \_ 処理の \_ 選択プロパティを (フィーダー &#x7c; DUPLEX &#x7c; front \_ first) に設定する必要があります。 この処理が完了すると、アプリケーションは、データ転送を要求する子項目に移動する必要があります。 ミニドライバーは、ADF の最初のページの前をページ1、ページ2として、ADF の2番目のページの前をページ3として報告します。

デバイスに ADF がある場合は、ADF のプロパティをサポートする必要があることに注意してください。
