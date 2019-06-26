---
title: UMDF ドライバーに対するセッション 0 のガイドライン
description: UMDF ドライバーに対するセッション 0 のガイドライン
ms.assetid: 67EF6762-AA31-4D35-8EB3-04F9CD34C7D1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3da3014f3ae3c8ea6e8c7cb59fec3b9db80c31af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376180"
---
# <a name="session-zero-guidelines-for-umdf-drivers"></a>UMDF ドライバーに対するセッション 0 のガイドライン


Windows Vista 以降、オペレーティング システムでは、サービスとそれ以降で実行中のアプリケーションにセッション 0 でシステム プロセス、上位の番号付きセッションを分離します。 UMDF ホスト プロセス (WUDFHost.exe) は、セッション 0 で実行されているシステム プロセスのいずれかであるために、UMDF ドライバーは、アプリケーションから分離されます。 結果としてには、ドライバーを開発するときに、次のガイドラインを使用する必要があります。

-   ダイアログ ボックスなどのユーザー インターフェイス (UI) 要素を作成したり、ユーザー入力に依存しないでください。 ユーザーがセッション 0 で実行されていないため、本人ことはありません、UI が表示されそれに応答することはできません。

    同様に、UI 要素を操作できません。 たとえば、UMDF ドライバーでは、ユーザーのセッションで windows を列挙できません。

-   ドライバーは、サービスと通信する必要がある場合、は、リモート プロシージャ コール (RPC) または名前付きパイプなどのクライアント/サーバー メカニズムを使用します。
-   Windows api 関数を呼び出すときは、注意を使用します。 一部の関数は、UI 要素を操作する可能性があります。 またはユーザーのセッションで名前付きオブジェクトにアクセスしようとしています。 ユーザー モード サービスから呼び出すことはありません Windows 関数を呼び出さないでください。 一般的な規則として UMDF ドライバーは user32.dll でエクスポートされた関数ではなく、kernel32.dll でエクスポートされた関数を安全に呼び出すことができます。

    UMDF ドライバーでは、次のタスクを実行する Windows 関数を呼び出すことがあります。

    -   ドライバーを呼び出すことができます **SetupDi * * * Xxx*プラグ アンド プレイ デバイスのプロパティを取得する関数。 たとえば、 [OSR USB Fx2 Learning kit UMDF ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?linkid=256202)呼び出し[ **SetupDiGetDeviceRegistryProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)デバイスのバスの種類の GUID を取得します。
        **注**  A UMDF ドライバーで安全に呼び出すさまざまなことはできません、**SetupDi * * * Xxx*デバイス ノードのプロパティを取得する関数の呼び出しに安全では、関数が。

         

    -   手動のキューからの I/O 要求を取得するドライバーは、キューをポーリングする定期的なタイマーを作成する場合があります。 たとえば、 [WudfVhidmini](https://go.microsoft.com/fwlink/p/?linkid=256226)サンプルでは、呼び出すことにより、タイマー コールバック ルーチンを登録します[ **CreateThreadpoolTimer**](https://docs.microsoft.com/windows/desktop/api/threadpoolapiset/nf-threadpoolapiset-createthreadpooltimer)、を呼び出すことによって定期的なタイマーを設定および[。 **SetThreadpoolTimer**](https://docs.microsoft.com/windows/desktop/api/threadpoolapiset/nf-threadpoolapiset-setthreadpooltimer)します。
        **注**  バージョン 1.11 以降、UMDF では、作業項目。 詳細については、次を参照してください。[を使用して作業項目](using-workitems.md)します。

         

Orwick の 14 (「以外のフレームワーク」) の章を参照してください、フレームワーク外でシステム サービスの使用に関する追加情報は、小額と Guy Smith。 *Windows Driver Foundation でのドライバーの開発*します。 Redmond、WA:Microsoft Press、2007 年。

Session 0 分離の詳細については、次を参照してください。[サービスと Windows でドライバーの影響の Session 0 分離](https://go.microsoft.com/fwlink/p/?linkid=240132)します。

 

 





