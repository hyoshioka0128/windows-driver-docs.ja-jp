---
title: デバイス オブジェクトの検証失敗
description: デバイス オブジェクトの検証失敗
ms.assetid: aa4abc20-0b87-44d7-8987-a5b2be397bb1
keywords:
- 信頼性の WDK カーネル、デバイス オブジェクトの検証
- デバイス オブジェクトの WDK カーネル、検証エラー
- 検証エラーの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 531fc5bbc64c16186b528a30cda00c01fc22530a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580780"
---
# <a name="failure-to-validate-device-objects"></a>デバイス オブジェクトの検証失敗





多くのドライバーを呼び出して 1 つ以上の種類のデバイス オブジェクトを作成する[ **IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)します。 一部のドライバーは、コントロール内のデバイス オブジェクトを作成、 **DriverEntry**ドライバー FDO を作成する前に、ドライバーと通信するアプリケーションを許可するルーチン。 たとえば、ファイル システム ドライバーとファイル システムとして自身を登録するときに、ファイル システムの通知を処理するためにデバイス オブジェクトを作成**IoRegisterFileSystem**します。

ドライバーに備える[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729)任意のデバイス オブジェクトの要求が作成されます。 成功の状態で要求を完了すると、ドライバーは、作成されたファイル オブジェクトのユーザーがアクセスできる、I/O 要求を受信すると予想されます。 その結果、1 つ以上のデバイス オブジェクトを作成する任意のドライバーは、各 I/O 要求を指定するデバイス オブジェクトをチェックする必要があります。

たとえば、ドライバーは内のデバイス オブジェクトの全体的なコントロールを作成します[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff544113)、別のデバイス オブジェクトのセットを作成し、その[ *AddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。 たとえば、 *AddDevice*ルーチンを下位レベルのドライバーに関する情報を含む、デバイスの拡張機能を初期化しますが、コントロールのデバイス オブジェクトにはこの情報は含まれません。 この場合、すべてのディスパッチ ルーチンは、受信した各デバイス オブジェクトをチェックしてくださいである必要があります。 それ以外の場合、デバイスの拡張機能の情報を使用しようとするときは、ドライバーがクラッシュする可能性があります。

 

 




