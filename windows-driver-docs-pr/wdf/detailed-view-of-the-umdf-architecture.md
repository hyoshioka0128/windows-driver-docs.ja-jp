---
title: UMDF のアーキテクチャ
description: このトピックでは、ドライバー マネージャーが、ユーザー モード デバイス スタックを構築する方法と、ホスト プロセス、リフレクタ、およびドライバー マネージャーのアプリケーションがユーザー モード ドライバー フレームワーク (UMDF) ドライバーに送信する I/O 要求を処理する方法について説明します。
ms.assetid: 118e5fe8-ba1e-4012-9632-fd92f4cee6f1
keywords:
- ユーザー モード ドライバー フレームワーク WDK のアーキテクチャ
- UMDF WDK、アーキテクチャ
- ユーザー モード ドライバー WDK UMDF、アーキテクチャ
- WDK UMDF のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fcb3c1b3c1e97bd588b8d99293f7f33972a0bad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377456"
---
# <a name="architecture-of-umdf"></a>UMDF のアーキテクチャ


このトピックでは、ドライバー マネージャーが、ユーザー モード デバイス スタックを構築する方法と、ホスト プロセス、リフレクタ、およびドライバー マネージャーのアプリケーションがユーザー モード ドライバー フレームワーク (UMDF) ドライバーに送信する I/O 要求を処理する方法について説明します。

カーネル モード スタックと同様に、構築とユーザー モードのスタックの破棄によって左右されますプラグ アンド プレイ (PnP) イベント。 カーネル モード スタックがビルドされたら、reflector は、ドライバー マネージャーは、ユーザー モードのスタックの構築を開始を通知します。 ドライバー マネージャーは、ドライバーのホスト プロセスを起動し、実行中のプロセス、ユーザー モードのスタックを構築するための十分な情報を提供します。 これにより、ユーザー モードのスタックと見なすカーネル モード スタックの拡張機能。

ドライバーのホスト プロセスでは、ドライバーとルートのメッセージをユーザー モードのスタック内のドライバーの間ユーザー モードの実行環境を提供します。 Reflector は、メッセージ ベースのプロセス間通信メカニズムを使用して、ドライバー マネージャーとホスト プロセスと通信します。

![reflector でデバイス オブジェクトと下矢印を含む umdf コンポーネント](images/umdfarch4.gif)

UMDF ドライバーに、I/O 要求を送信するアプリケーションなどの呼び出し、Win32 ファイル I/O 関数では、 [ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **ReadFileEx**、 **CancelIoEx**、または[ **DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)します。 Reflector は、クライアント アプリケーションから要求を受信したときに、適切なドライバーのホスト プロセスに要求を送信します。 ドライバー ホスト要求を処理し、ルート、適切なユーザー モード デバイス スタックの先頭にします。

要求がユーザー モードのスタック内のドライバーのいずれかで完了したか、ドライバーを reflector のいずれかによって転送されます。 Reflector は、ユーザー モード ドライバー スタックからの要求を受信したときに、完了のカーネル モード スタック ダウン要求を送信します。

 

 





