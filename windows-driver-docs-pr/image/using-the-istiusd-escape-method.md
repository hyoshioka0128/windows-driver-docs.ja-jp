---
title: IStiUSD エスケープ メソッドの使用
description: IStiUSD エスケープ メソッドの使用
ms.assetid: f9b1ede6-8311-4cc9-8bf7-20018cb35a3d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 480aff9db018cbd4dcc131e5132ae1430ae7a9de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375384"
---
# <a name="using-the-istiusd-escape-method"></a>IStiUSD エスケープ メソッドの使用





[ **IStiUSD::Escape** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape)ハードウェアに直接情報を渡すメソッドが呼び出されます。 このメソッドは、Windows XP およびそれ以降のオペレーティング システムでのみサポートされます。

データ ソースのマネージャーに TWAIN と互換性のあるアプリケーションと、WIA ドライバーの間のすべての通信は最初 (*twain\_32. dll*)、TWAIN 互換性レイヤーをさらに呼び出し (*wiadss.dll*). TWAIN 互換性レイヤーを呼び出して、WIA ドライバーの[ **IStiUSD::Escape** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-escape)メソッド、およびメソッドに次の 2 つのエスケープ コードのパス 1 つ。

[ESC\_TWAIN\_機能エスケープ コード](esc-twain-capability-escape-code.md)

[ESC\_TWAIN\_プライベート\_サポートされている\_CAP エスケープ コード](esc-twain-private-supported-caps-escape-code.md)

TWAIN アプリケーションでは、WIA ドライバーのプライベート機能の一覧を要求、TWAIN 互換レイヤー呼び出し、ドライバーの**IStiUSD::Escape** esc キーを渡してメソッド\_TWAIN\_プライベート\_サポートされている\_呼び出しでの上限。 TWAIN 互換レイヤーの静的を返します、ドライバーがパススルー機能をサポートしていない場合 (既定値) の機能の一覧。 それ以外の場合、ドライバーは、TWAIN 互換性レイヤーをプライベートのサポートされる機能の一覧を返します。

TWAIN 互換レイヤー TWAIN アプリケーションでは、既に TWAIN 互換性レイヤーの既定のリストされていない機能の操作を送信する呼び出し、ドライバーの**IStiUSD::Escape**メソッド、escキーを渡してこの時間\_TWAIN\_呼び出しで機能します。

ただし、前述の説明はややごく簡単に説明します。 TWAIN 互換レイヤーが、ドライバーの 2 つの呼び出しにより、実際には、ドライバーのプライベート機能の一覧については、TWAIN アプリケーションが表示されたら、 **IStiUSD::Escape**メソッド。 最初の呼び出しでは、TWAIN 互換レイヤーは、メモリの量は、機能の一覧を格納するために必要な WIA ドライバーで確認します。 TWAIN 互換レイヤーは、WIA ドライバーを使用するためのメモリの量を割り当てます。 2 番目の呼び出しでは、TWAIN 互換レイヤーは、WIA ドライバーは、前述のメモリにコピーする機能一覧については、WIA ドライバーを要求します。 TWAIN 互換レイヤーは、割り当てと TWAIN WIA トランザクションで使用されるすべてのメモリを解放します。 この配置では、WIA ドライバーが TWAIN 互換性レイヤーを使用してメモリを解放することを防ぎます。

TWAIN 互換レイヤーは、ドライバーのも呼び出して**IStiUSD::Escape**メソッドを 2 回と ESC\_TWAIN\_機能が渡され、対象の目的は、機能の 1 つを取得します。 最初の呼び出しは、機能を格納するために必要なメモリの量 WIA ドライバーを確認し、2 番目の呼び出しが、機能を返します。 機能の設定操作を必要とする単一の呼び出しのみ**IStiUSD::Escape**メモリを割り当てる必要がないためです。

すべての呼び出しを**IStiUSD::Escape**メソッドは、この順序で検証する必要があります。

1.  検証、 *EscapeFunction*関数コード。 その情報が有効でない場合ですぐに失敗します。 これにより、不適切なコードは、ドライバーで処理されているできなくなります。

2.  検証、受信バッファー *lpInData*します。 その情報が有効でない場合ですぐに失敗します。 無効な受信バッファーには、WIA ドライバーがクラッシュする可能性があります。

3.  送信バッファーの検証*pOutData*します。 その情報が有効でない場合ですぐに失敗します。 ドライバーは、必要なデータを記述することで、要求を完了することはできない場合、は、データを処理することは必要はありません。

4.  送信バッファーのサイズを検証します。 場合は、ドライバーは、送信バッファーに適量のデータを書き込むことはできませんは、そのデータできません正しく、呼び出し元に処理します。

コード サンプルでは、次のセクションでは、パスの使用方法を示します-ただし、プライベートの機能を備えた TWAIN アプリケーションをサポートする機能。 コード サンプルを使用して、ヘッダー ファイルで定義されている 2 つのエスケープ コード*wiatwcmp.h*、ESC\_TWAIN\_プライベート\_サポートされている\_CAP と ESC\_TWAIN\_機能します。

[ESC\_TWAIN\_プライベート\_サポートされている\_CAP エスケープ コード](esc-twain-private-supported-caps-escape-code.md)

[ESC\_TWAIN\_機能エスケープ コード](esc-twain-capability-escape-code.md)

 

 




