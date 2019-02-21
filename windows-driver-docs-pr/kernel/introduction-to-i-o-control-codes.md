---
title: I/O 制御コードの概要
description: I/O 制御コードの概要
ms.assetid: 8b9e09ef-56f9-42b9-9b65-04bc380f3a1e
keywords:
- I/O 制御コード WDK カーネルでは、I/O 制御コードについて
- 制御コード WDK の Ioctl I/O 制御コードについて
- I/O 制御コードの詳細について、Ioctl WDK カーネル
- プライベートの Ioctl WDK カーネル
- パブリックの Ioctl WDK カーネル
- Ioctl WDK ユーザー モード
- ユーザー モード コンポーネント WDK Ioctl
- I/O 制御コード WDK ユーザー モード
- 制御コード WDK ユーザー モード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1425338b7af965a9936ab445735209482b0f5dd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531576"
---
# <a name="introduction-to-io-control-codes"></a>I/O 制御コードの概要





I/O 制御コード (Ioctl) は、ユーザー モード アプリケーションやドライバーの間の通信、または内部的には、スタックのドライバー間の通信に使用されます。 Irp を使用して I/O 制御コードが送信されます。

ユーザー モード アプリケーションは、ドライバーを Ioctl を呼び出して送信[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)、Microsoft Windows SDK のドキュメントに記載されています。 呼び出す**DeviceIoControl** I/O マネージャーの作成が発生する、 [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)を要求し、送信します。最上位のドライバーです。

さらに、上位レベルのドライバー Ioctl に送信下位レベルのドライバーを作成および送信**IRP\_MJ\_デバイス\_コントロール**または[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)要求。 ドライバーでこれらの要求を処理する[ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ *DispatchInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 (ユーザー モード アプリケーションを送信できません**IRP\_MJ\_内部\_デバイス\_コントロール**要求します)。

Ioctl には"public"と"private"がいくつか。 通常パブリック Ioctl がシステム定義し、Windows Driver Kit (WDK) または Windows SDK のいずれかで、マイクロソフトが記載されています。 ユーザー モード コンポーネントの呼び出しを使用して、送信される[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)、または間を使用して 1 つのカーネル モード ドライバーから送信が**IRP\_MJ\_デバイス\_コントロール**または**IRP\_MJ\_内部\_デバイス\_コントロール**要求。 パブリック Ioctl の例として、 [SCSI ポート I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff565367)と[I8042prt マウス内部デバイス制御要求](https://msdn.microsoft.com/library/windows/hardware/ff539982)します。

その一方で、プライベート Ioctl では、互いに通信するベンダーのソフトウェア コンポーネントによって排他的に使用するものです。 プライベート Ioctl では、通常はベンダーから提供されたヘッダー ファイルで定義し、パブリックに記載されていません。 これらのパブリックの Ioctl などへのユーザー モード コンポーネントの呼び出しを使用して送信が[ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)、または間を使用して 1 つのカーネル モード ドライバーから送信が**IRP\_MJ\_デバイス\_コントロール**または**IRP\_MJ\_内部\_デバイス\_コントロール**要求。

パブリックおよびプライベートの Ioctl のコーディングとの間の違いはありません。 ただし、システム定義の Ioctl に使用されるものと比較して、ベンダー定義の Ioctl で使用できる内部のコードの違いがあります。 使用可能なパブリック Ioctl はニーズに適合しない場合は、あなたのソフトウェア コンポーネントが相互に通信に使用できる新しいプライベート Ioctl を定義できます。 詳細については、次を参照してください。 [I/O 制御コードを定義する](defining-i-o-control-codes.md)します。

 

 




