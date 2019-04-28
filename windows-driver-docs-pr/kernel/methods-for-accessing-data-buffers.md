---
title: データ バッファーにアクセスする方法
description: データ バッファーにアクセスする方法
ms.assetid: f95a0aec-65f9-44c9-8ae5-11bb4d832752
keywords:
- I/O WDK カーネルでは、データ バッファー
- データ バッファーの WDK I/O
- WDK の I/O バッファー
- WDK の I/O バッファーにアクセスします。
- WDK の I/O バッファーのデータにアクセスします。
- データ転送の WDK カーネル、データ バッファーへのアクセス
- WDK カーネルのデータを転送するには、データ バッファーへのアクセス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a6a23ca1b45d98da0b0433006d18f17d0c4e4b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380366"
---
# <a name="methods-for-accessing-data-buffers"></a>データ バッファーにアクセスする方法


ユーザー モード アプリケーションとシステムのデバイス間でデータを転送ドライバー スタックの主な責務のいずれかです。 オペレーティング システムでは、データ バッファーにアクセスするため次の 3 つのメソッドを提供します。

<a href="" id="buffered-i-o"></a>*バッファー内の I/O*  
オペレーティング システムでは、アプリケーションのバッファーのサイズと等しいページングされないシステムのバッファーを作成します。 書き込み操作の場合は、I/O マネージャーは、ドライバー スタックを呼び出す前に、システムのバッファーにユーザー データをコピーします。 読み取り操作は、I/O マネージャーからデータをコピー、システムのバッファーには、アプリケーションのバッファーにドライバー スタックが、要求された操作を完了後します。

詳細については、次を参照してください。[を使用してバッファー I/O](using-buffered-i-o.md)します。

<a href="" id="direct-i-o"></a>*ダイレクト I/O*  
オペレーティング システムでは、メモリ内アプリケーションのバッファーをロックします。 ロックされたメモリのページを識別し、ドライバー スタックに MDL を渡しますメモリ記述子一覧 (MDL) が作成されます。 ドライバーは、ロックされたページを MDL を通じてアクセスします。

詳細については、次を参照してください。[を使用して直接 I/O](using-direct-i-o.md)します。

<a href="" id="neither-buffered-nor-direct-i-o"></a>*バッファーもダイレクト I/O*  
オペレーティング システムでは、ドライバー スタックに、アプリケーションのバッファーの仮想の開始アドレスとサイズを渡します。 バッファーには、アプリケーションのスレッドのコンテキストで実行されるドライバーからアクセスできるのみです。

詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](using-neither-buffered-nor-direct-i-o.md)します。

[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)要求ドライバーは、それぞれにフラグを使用して、I/O メソッドを指定[**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)構造体。 詳細については、次を参照してください。[デバイス オブジェクトを初期化して](initializing-a-device-object.md)します。

[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766) I/O メソッドは、要求によって決まります、 *TransferType* IOCTL の各値に含まれる値。 詳細については、次を参照してください。 [I/O 制御コードを定義する](defining-i-o-control-codes.md)します。

ドライバー スタックのすべてのドライバーする必要があります要求ごとに同じバッファーへのアクセス メソッドを除く可能性がありますドライバーの使用、最上位レベル (を下位のドライバーで使用される方法に関係なく、「も」メソッドを使用することができます)。

 

 




