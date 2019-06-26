---
title: SAN ソケットを閉じる
description: SAN ソケットを閉じる
ms.assetid: 49224987-ed46-4631-a47b-70cd855cfa40
keywords:
- ソケットを閉じる、WDK の SAN
- ソケットの SAN を閉じる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dbda47fae7a0ce31f929b92eb3d6d8c06be7c0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384220"
---
# <a name="closing-a-san-socket"></a>SAN ソケットを閉じる





接続の両側に SAN サービス プロバイダーの呼び出し Windows Sockets をオンにした後[ **WSPCloseSocket** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566273(v=vs.85))関数の場合、SAN サービス プロバイダーは SAN のソケットを閉じるには、次の手順を実行します。:

1.  接続の両側で各 SAN サービス プロバイダーの接続を廃棄し、完了--要求を受信[ **WSPRecv** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566309(v=vs.85)) で適切なエラーコードを返すことによって関数呼び出し。*lpErrno*パラメーター。 たとえば、SAN サービス プロバイダーは、リモート ピアが接続をリセットすることを示す WSAECONNRESET を返します。

    各 SAN サービス プロバイダーも保留中の SAN ソケットを閉じるの重複した操作の完了を通知します。 SAN サービス プロバイダーの呼び出し、 **WPUCompleteOverlappedRequest**オーバー ラップ処理の完了を通知する関数。 この呼び出しで SAN サービス プロバイダーがへのポインターを渡す、 [ **WSAOVERLAPPED** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565952(v=vs.85))オーバー ラップされた操作に関連付けられている構造体。 SAN サービス プロバイダーにも渡すします WSA\_操作\_SAN ソケットが閉じられたので、オーバー ラップ処理が取り消されましたことを指定するエラー コードを中断します。 オーバー ラップ処理の完了を通知する前に SAN サービス プロバイダーは、操作に必要だったすべてのメモリを解放する必要があります。

2.  SAN サービス プロバイダーがアップ-呼び出す--を完了した後が付いている関数を呼び出す**WPU**-SAN ソケットを介して取得されたハンドルを使用して、スイッチに、 **WPUCreateSocketHandle**を呼び出し、SAN サービス プロバイダーに加える必要が最終的なアップ呼び出しスイッチを呼び出して、 **WPUCloseSocketHandle**ソケット ハンドルを閉じます。 SAN は、サービス プロバイダーにし、SAN のソケットに関連するものすべてをクリーンアップします。 アップ呼び出しは、スイッチのアップ呼び出しのディスパッチ テーブルからの関数呼び出しです。 SAN サービス プロバイダーの呼び出し時にこのアップ呼び出しのディスパッチ テーブルへのポインターを提供[ **WSPStartupEx** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566321(v=vs.85))プロバイダーの使用を開始する関数。 これらを呼び出す関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

SAN サービス プロバイダーは、SAN のソケットを閉じるには、前の手順を実行する限り、他のすべてのスイッチによって行われます。

SAN サービス プロバイダーとソケットのクロージャを開始するスイッチの間の競合状態を防ぐためには、SAN サービス プロバイダーはスイッチ呼び出されるまで、SAN のソケットに関連するデータ構造を解放する必要がありますしない**WSPCloseSocket**します。

 

 





