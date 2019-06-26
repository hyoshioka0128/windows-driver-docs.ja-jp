---
title: HID コレクションを開く
description: このセクションでは、HID クラス ドライバー、デバイスの HID コレクションを操作するには、(HIDClass) を使用した HID クライアントと通信する方法について説明します。
ms.assetid: 97550D1D-2C37-4996-8522-DB18B1AA3C4A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aeeb3cfa09ae604c3394e1bed9c6fae0be2f601
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366252"
---
# <a name="opening-hid-collections"></a>HID コレクションを開く


このセクションでは、HID クラス ドライバー、デバイスの HID コレクションを操作するには、(HIDClass) を使用した HID クライアントと通信する方法について説明します。

HID のクライアントは、次のモードで動作できます。

-   アプリケーション/ドライバーの使用-モード
-   カーネル モード ドライバー

次のセクションでは、HIDClass 上記のいずれかのモードを使用すると、HID クライアントと通信する方法を特定します。

このセクションでは、ユーザー モード アプリケーションとカーネル モード ドライバーの動作方法について説明します[HID コレクション](hid-collections.md)します。

一般に、ユーザー モード アプリケーションは、次を行います。

- 呼び出し[デバイスのインストール機能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))(**SetupDi * * * Xxx*関数) を見つけ、HID コレクションを識別します。

- HID コレクションでファイルを開くに CreateFile が呼び出されます。

- 呼び出し**HidD\_** <em>Xxx</em> HID のコレクションを取得するルーチンをサポートする HID [preparsed データ](preparsed-data.md)と HID コレクションに関する情報。

- 入力のレポートの読み取りを ReadFile や WriteFile 出力レポートを送信するを呼び出します。

- 呼び出し**HidP\_** <em>Xxx</em> HID HID レポートを解釈するためのルーチンをサポートします。

一般に、カーネル モード ドライバーは、次を行います。

- 検索して、HID コレクションを識別します。

  ドライバーが関数またはフィルター ドライバーの場合は、コレクションのデバイスのスタックに既にアタッチされています。 ただし、ドライバーが、コレクションのデバイスのスタックにアタッチされていない場合、ドライバーは[プラグ アンド プレイの通知を使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-pnp-notification)します。

- 使用して、 [ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create) HID コレクションを開く要求

- IOCTL を使用して\_HID\_*Xxx* HID コレクションの preparsed データおよび HID コレクションに関する情報を取得する要求

- 使用して[ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)入力レポートの読み取り要求と[ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)出力レポートを送信する要求

- 呼び出し**HidP\_** <em>Xxx</em> HID HID レポートを解釈するためのルーチンのサポート

HID コレクションの動作の詳細についてを参照してください。

[検索して HID コレクションを開く](finding-and-opening-a-hid-collection.md)

[HID コレクションのセキュリティで保護された読み取りの適用](enforcing-a-secure-read-for-a-hid-collection.md)

[Preparsed データを取得します。](obtaining-preparsed-data.md)

[コレクションの情報を取得します。](obtaining-collection-information.md)

[HID レポートの処理](handling-hid-reports.md)

[リソースの解放](freeing-resources.md)

 

 




