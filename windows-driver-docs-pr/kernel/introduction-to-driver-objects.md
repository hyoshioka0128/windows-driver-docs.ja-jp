---
title: ドライバー オブジェクトの概要
description: ドライバー オブジェクトの概要
ms.assetid: 497ee2dc-671d-408e-b228-16dc24532375
keywords:
- ドライバー オブジェクトの WDK カーネル
- 標準のドライバー ルーチン WDK カーネル ドライバー オブジェクト
- ドライバー ルーチン WDK カーネル ドライバー オブジェクト
- ルーチン WDK カーネル ドライバー オブジェクト
- WDK ドライバー オブジェクトのオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc774035d74293006a46c5f1abdb910391abaa56
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341026"
---
# <a name="introduction-to-driver-objects"></a>ドライバー オブジェクトの概要


## <a href="" id="ddk-introduction-to-driver-objects-kg"></a>


I/O マネージャーを作成、*ドライバー オブジェクト*各ドライバーのインストールして読み込まれます。 使用してドライバー オブジェクトが定義された[**ドライバー\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff544174)構造体。

I/O マネージャーがドライバーを呼び出すときに[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113) 、日常的なドライバーのドライバー オブジェクトのアドレスはすべて提供します。 ドライバーのオブジェクトには、ドライバーの標準的な手順の多くへのエントリ ポイントの記憶域が含まれています。 ドライバーは、これらのエントリ ポイントを入力します。

## <a href="" id="driver-object-illustration"></a>


次の図は、最下位レベルで高度なドライバーが必要がありますまたはできるシステム定義の標準的なルーチンのセットでのドライバー オブジェクトを示しています。

I/O 要求パケット (IRP) は、その名の横にアスタリスクで標準的な各ルーチンは、入力として受け取ります。 これらの各標準ルーチンは、I/O 要求の対象のデバイス オブジェクトへのポインターも受信します。

![ドライバー オブジェクトを示す図](images/24drvobj.png)

I/O マネージャーは、ドライバー オブジェクトの種類を定義し、ドライバーのオブジェクトを使用して登録して、ドライバーの読み込まれるイメージに関する情報を追跡します。 ディスパッチのエントリ ポイントに注意してください (**DDDispatch * * * Xxx*を通じて**DDDispatch * **Yyy*) ドライバー オブジェクトでは、主要な関数のコードに対応 (** IRP\_MJ\_* XXX * * *) が渡され、Irp の I/O スタックの場所。

I/O マネージャーは、ドライバーが指定したディスパッチ ルーチンに最初に各 IRP をルーティングします。 最下位レベル ドライバーのディスパッチ ルーチンは、通常、I/O サポート ルーチンを呼び出します ([**IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)) キュー (または渡す) ドライバーに有効な引数を持つ各 IRP [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン。 *StartIo*ルーチンが特定のデバイスで要求された I/O 操作を開始します。 通常より高度なドライバーを持っていません*StartIo*ルーチンが、以下のことができます。

 

 




