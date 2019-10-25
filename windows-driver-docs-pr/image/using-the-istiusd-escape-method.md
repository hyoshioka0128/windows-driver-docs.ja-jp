---
title: IStiUSD エスケープ メソッドの使用
description: IStiUSD エスケープ メソッドの使用
ms.assetid: f9b1ede6-8311-4cc9-8bf7-20018cb35a3d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eccea0d85fad4d376ee7c69bae100e6642802a9f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840726"
---
# <a name="using-the-istiusd-escape-method"></a>IStiUSD エスケープ メソッドの使用





情報を直接ハードウェアに渡すために、 [**ib usd:: Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)メソッドが呼び出されます。 この方法は、Windows XP 以降のオペレーティングシステムでのみサポートされています。

TWAIN 互換のアプリケーションと WIA ドライバー間のすべての通信は、まずデータソースマネージャー (*twain\_32 .dll*) に送信され、さらに twain 互換性レイヤー (*wiadss .dll*) が呼び出されます。 次に、TWAIN 互換レイヤーは、WIA ドライバーの[**Ib usd:: escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)メソッドを呼び出し、次の2つのエスケープコードのいずれかをメソッドに渡します。

[ESC\_TWAIN\_機能エスケープコード](esc-twain-capability-escape-code.md)

[ESC\_TWAIN\_プライベート\_サポートされている\_CAPS エスケープコード](esc-twain-private-supported-caps-escape-code.md)

Twain アプリケーションが WIA ドライバーのプライベート機能一覧を要求すると、TWAIN 互換性レイヤーはドライバーの**Ib usd:: Escape**メソッドを呼び出し、ESC\_TWAIN\_private\_呼び出しでサポートされている\_キャップを渡します。 ドライバーがパススルー機能をサポートしていない場合は、TWAIN 互換レイヤーの静的 (既定) 機能の一覧が返されます。 それ以外の場合、ドライバーはサポートされているプライベート機能の一覧を TWAIN 互換性レイヤーに返します。

Twain アプリケーションが、まだ TWAIN 互換レイヤーの既定のリストに含まれていない機能操作を送信する場合、TWAIN 互換性レイヤーはドライバーの**Ib usd:: Escape**メソッドを呼び出します。今回は、ESC\_twain に渡し\_呼び出しの機能。

ただし、前述の説明はやや単純化されています。 TWAIN アプリケーションからドライバーのプライベート機能リストが要求されると、TWAIN 互換性レイヤーは実際には、ドライバーの**ib usd:: Escape**メソッドに対して2回呼び出しを行います。 最初の呼び出しでは、TWAIN ドライバーに、機能一覧を格納するために必要なメモリ量が要求されます。 その後、TWAIN 互換性レイヤーによって、WIA ドライバーが使用するメモリ量が割り当てられます。 2番目の呼び出しでは、TWAIN ドライバーが機能一覧を要求し、WIA ドライバーは前に説明したメモリにコピーします。 Twain 互換性レイヤーは、TWAIN トランザクションで使用されるすべてのメモリの割り当てと解放を担当します。 これにより、TWAIN ドライバーは、TWAIN 互換レイヤーで使用しているメモリを解放できなくなります。

また、TWAIN 互換性レイヤーは、ESC\_TWAIN\_機能が渡され、機能を取得する目的である場合に、ドライバーの**ib usd:: Escape**メソッドを2回呼び出します。 最初の呼び出しでは、機能を格納するために必要なメモリの量が WIA ドライバーに要求され、2回目の呼び出しでは機能が返されます。 SET 機能操作では、メモリを割り当てる必要がないため、 **i、usd:: Escape**を1回だけ呼び出す必要があることに注意してください。

**It usd:: Escape**メソッドのすべての呼び出しは、次の順序で検証する必要があります。

1.  *EscapeFunction*関数のコードを検証します。 有効でない場合は、すぐに失敗します。 これにより、ドライバーで正しくないコードが処理されるのを防ぐことができます。

2.  受信バッファー、 *Lpindata*を検証します。 有効でない場合は、すぐに失敗します。 無効な受信バッファーが原因で、WIA ドライバーがクラッシュする可能性があります。

3.  送信バッファー、 *Poutdata*を検証します。 有効でない場合は、すぐに失敗します。 ドライバーが必要なデータを書き込んで要求を完了できない場合、そのデータを処理する必要はありません。

4.  送信バッファーのサイズを検証します。 ドライバーが送信バッファーに適切な量のデータを書き込むことができない場合、呼び出し元はそのデータを適切に処理できません。

次のセクションのコードサンプルでは、プライベート機能を備えた TWAIN アプリケーションをサポートする、パススルー機能の使用方法について説明します。 このコードサンプルでは、ヘッダーファイル*wiatwcmp .h*に定義されている2つのエスケープコード、ESC\_TWAIN\_PRIVATE\_サポートされている\_CAPS と ESC\_TWAIN\_機能を使用します。

[ESC\_TWAIN\_プライベート\_サポートされている\_CAPS エスケープコード](esc-twain-private-supported-caps-escape-code.md)

[ESC\_TWAIN\_機能エスケープコード](esc-twain-capability-escape-code.md)

 

 




