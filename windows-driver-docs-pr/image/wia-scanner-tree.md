---
title: WIA スキャナー ツリー
description: WIA スキャナー ツリー
ms.assetid: bd1452b9-1926-4dd6-b94c-e44f07573266
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcaa5c3e781f9306a4939f7c5e32c272c972ba98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840668"
---
# <a name="wia-scanner-tree"></a>WIA スキャナー ツリー





次の図は、スキャナーとそれが生成したイメージを示しています。

![スキャナーとそれが生成したイメージを示す図](images/art-scanner.png)

次の図は、Microsoft Windows Me または Windows XP スキャナー、またはスキャナーにドキュメントフィーダー、両面印刷用スキャナーがない場合の windows Vista のスキャナーを示しています。

次の図に示すように、WIA は、前の図で示されているスキャナーとそのイメージを項目ツリーとして表します。

![wia がスキャナーとそのイメージを項目ツリーとして表す方法を示す図](images/art-4.png)

スキャナー自体であるルート項目は、一般的なデバイスプロパティ (カメラとスキャナーの両方に共通のプロパティ) とスキャナー固有のデバイスプロパティで構成されています。 同様に、各子項目は、カメラとスキャナーの両方の項目に共通するプロパティだけでなく、スキャナー項目に固有のプロパティで構成されます。

アプリケーションでは、WIA サービスを使用して、次の項目をスキャナー項目から要求できます。

-   クエリスキャナー機能。

-   スキャナーデバイスのプロパティを設定します。

-   データ転送を要求します。

Windows Me と Windows XP では、ルート項目のすぐ下に、一般的なスキャナーオブジェクトには、デバイスのデータ収集機能を表すスキャナー項目という1つの項目があります。 アプリケーションは、スキャナー項目のプロパティを設定することによって、スキャンを設定します。 スキャンは、アプリケーションが、WIA サービスを介して項目からデータを要求したときに実行されます。

Windows Me と Windows XP では、通常、アプリケーションは、2つの項目 (ルート項目と1つの子) で表されるように、自動ドキュメントフィーダー (ADFs) を備えたスキャナーなどのフラットベッドスキャナーを必要とします。 すべてのデータ転送は、子項目から実行されます。 ドライバーは、プライベートに使用するために他の項目を作成することができます。これらの項目は、転送可能にすることができます。 (これを行うには、 [**wiasCreateChildAppItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem)への呼び出しで item type フラグの WiaItemTypeTransfer ビットを設定します。 この定数については、Microsoft Windows SDK のドキュメントを参照してください)。ただし、通常、アプリケーションはこれらのプライベート項目を認識しないため、それらを操作する方法がわかりません。 ADF を使用したスキャナーの場合、Windows Me または Windows XP では、スキャナーのルート項目に\_\_*XXX*プロパティを処理する WIA\_DPS\_ドキュメントを追加することにより、adf 機能が公開および制御されます。子項目。 これらのプロパティの詳細については、「 [WIA のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties)」を参照してください。 Windows Vista の ADF を使用したスキャナーの詳細については、「 [WIA フィーダースキャナー](wia-feeder-scanners.md)」を参照してください。

デバイスにフラットベッドおよび ADF が搭載されていて、Windows Me または Windows XP で双方向スキャンを実行できる場合、ドライバーは、\_機能のプロパティを[**処理する\_\_ドキュメントの WIA\_DPS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)を報告します (フィード |FLAT |DUP)。 [**WIA\_DPS\_ドキュメント\_処理\_選択**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)の有効な値が正しく設定されていることを確認します。 1つのスキャンジョブでスキャンされたすべてのドキュメントが、項目ツリーの単一の子項目に存在することに注意してください。 ADF を備えたスキャナーと Windows Vista の両面印刷装置の詳細については、「 [WIA フィーダースキャナー](wia-feeder-scanners.md)」を参照してください。

たとえば、アプリケーションが ADF から3ページの両面スキャンを実行するとします。 これを実現するために、アプリケーションでは、WIA\_DPS\_ドキュメント\_処理\_SELECT プロパティを (フィーダー |) に設定します。また、[ [**WIA\_DPS\_PAGES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages) ] プロパティを3に設定します。 アプリケーションで最初にページの先頭をスキャンする場合は、WIA\_DPS\_ドキュメント\_処理\_SELECT プロパティを設定する必要があります (フィーダー |両面 |FRONT\_最初)。 この処理が完了すると、アプリケーションは、データ転送を要求する子項目に移動する必要があります。 ミニドライバーは、ADF の最初のページの前をページ1、ページ2として、ADF の2番目のページの前をページ3として報告します。

デバイスに ADF がある場合は、ADF のプロパティをサポートする必要があることに注意してください。

 

 




