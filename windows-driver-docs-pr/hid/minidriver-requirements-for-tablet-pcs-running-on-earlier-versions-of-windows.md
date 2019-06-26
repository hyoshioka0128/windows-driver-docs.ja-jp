---
title: タブレット PC のミニドライバーの要件
description: ペン デバイスとボタンのデバイスのベンダーから提供された HID ミニドライバーの一般的な要件について説明します。
ms.assetid: 89BE7E13-4D46-4265-9522-D5A51999F633
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d301b456f368a98579f8012770c596a63902323
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371944"
---
# <a name="minidriver-requirements-for-tablet-pcs-running-on-earlier-versions-of-windows"></a>ミニドライバーの要件の以前のバージョンの Windows で実行されている Pc をタブレットします。


このセクションでは、Windows 8 より前のオペレーティング システムに適用し、デバイスのペンと tablet PC edition のシステムにインストールされているボタン デバイスのベンダーから提供された HID ミニドライバーの一般的な要件について説明します。

このセクションでは、ペンとボタンのデバイスについて説明します。

-   ペン デバイスについては、統合、Tablet PC の LCD ディスプレイおよびスタイラス ペンの動きをキャプチャするために使用します。
-   ボタン デバイスは、ペン デバイスを補足するものし、ボタンの入力をキャプチャするために使用します。 Tablet PC の詳細については、Windows XP Tablet PC Edition の web サイトを参照してください。

Tablet PC の詳細については、次を参照してください。、 [Windows XP Tablet PC Edition](https://go.microsoft.com/fwlink/p/?linkid=275069) web サイト。

Tablet PC をサポートするシステム提供のソフトウェアの詳細については、Microsoft Windows SDK の Tablet PC のドキュメントを参照してください。

ペンとボタンのデバイスは、HIDClass デバイス セットアップ クラスに属しています。 これらのデバイスは、システム提供によって運営されて[クライアント ドライバーの HID](hid-client-drivers.md)、HID ミニドライバーに関連付けられています。 デバイスのハードウェア インターフェイスをサポートするシステム提供の HID ミニドライバーがない場合は、ベンダーから提供されたの HID ミニドライバーが必要です。 デバイスはユーザー モードから API を使用して、システムが指定した Tablet PC、Windows SDK のドキュメントに記載されている運用します。

### <a name="requirements-for-pc-pen-devices"></a>PC のペン デバイスの要件

Tablet PC のペン デバイスが必要です。

-   使用状況 ページはデジタイザーとペンの使用は、最上位のコレクションを提供 (を参照してください[HID の使用](hid-usages.md))。

-   Tablet PC に組み込みマウスが含まれていない場合、Tablet PC のペン デバイスは最上位のコレクションの使用状況 ページが Generic Desktop との使用は、マウスを提供する必要があります。 マウス コレクションの目的は、システムのマウス カーソルを有効にするのにです。 ただし、マウス コレクションは入力レポートを生成する必要があります。 唯一の入力、ペン コレクションからは、カーソルの動きを使用してください。 (がインストールされているマウス デバイス、タブレット PC のオペレーティング システムが起動する場合、システムがマウス カーソルが表示されないとマウス デバイスとして、ペン コレクションを処理しません。)

-   生データのみを報告します。 ドライバーは、直線、ペンの傾き、画面の回転、またはスケーリングの補償されない必要があります。 これらの変換は、Tablet PC API によって処理されます。 ただし、ドライバーでは、ペンの座標システムで API で使用すると同じの原点と方向を使用する必要がありますを確認します。 たとえば、ドライバーする必要があります、配信元が、左から右、x 座標が増加する横長画面の左上隅であると y 座標を上から下に増えることを確認します。

-   デバイスが USB デバイスの場合は、Tablet PC のペン デバイスをサポートする必要があります、 [USB のセレクティブ サスペンド機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

### <a href="" id="ddk-requirements-on-hid-minidrivers-for-tablet-pc-button-devices-kg"></a>PC のボタンのデバイスの要件

Tablet PC ボタンのデバイスでは、Tablet pc のペン入力を補足します。 ボタン デバイスには、1 つまたは複数のボタンがサポートしています。 ボタン デバイス Tablet PC にインストールされている必要があります。

-   (Microsoft Windows SDK のドキュメントで説明) と Secure Attention シーケンス (SAS) の 1 つの専用ボタンを提供します。

-   ボタンが押されたときにイベントを生成するボタンが離されたときのイベント。

-   同時に押された状態またはリリースがボタンの数に関係なく、ボタンごとに個別のボタンのイベントを報告します。

-   使用状況のページでは Generic Desktop との使用は、キーボードの最上位のコレクションを提供 (を参照してください[HID の使用](hid-usages.md))。 キーボード コレクションは、SAS ボタン イベントのレポートにのみ使用されます。 SAS ボタンが押されたときに、以下の使用法を報告する必要があります。左側のコントロールは左 alt キーを押し、し、削除します。

-   使用状況のページでは Generic Desktop との使用は、Tablet PC System Controls の最上位のコレクションを提供します。 ボタンのイベントは、ボタン配列の使用状況 ページには、ボタンとボタンの数を 1 から使用状況の値の範囲を使用して報告されます。

 

 




