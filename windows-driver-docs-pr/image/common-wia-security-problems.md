---
title: WIA セキュリティ上の一般的な問題
description: WIA セキュリティ上の一般的な問題
ms.assetid: d3f7d6e9-1ac4-4209-92bb-d08e4e13a4ad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc9c2b087f16b71f8a59f5f570a2dd1110d98e5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571958"
---
# <a name="common-wia-security-problems"></a>WIA セキュリティ上の一般的な問題





既存の WIA ドライバーを妨げる可能性のあるいくつかの一般的な問題がある (で正しく動作していた**LocalSystem**) で正常に実行してから、 **LocalService**アカウント。

最も一般的な問題が発生します。

-   ファイル システムへのアクセス

    **LocalService**アカウントが、ファイルへのアクセスと厳しく制限されています。 たとえば、ドライバーは、% を書き込むことができなく*windir*% ディレクトリ。

-   レジストリへのアクセス

    多くのレジストリ キーを開いていた**LocalSystem**アカウントは、読み取り専用に**LocalService**します。 たとえば、ドライバーでは、HKLM サブツリー下のレジストリ キーに書き込むことが不要になったです。

-   名前付きカーネル オブジェクト

    適切な Acl がある、WIA ドライバーと、バンドルされているアプリケーションなどの外部コンポーネントによってアクセスされるオブジェクト (たとえば、イベントおよびミュー テックス) という名前を確認します。 アプリケーションは、名前付きイベント オブジェクトを作成しますへのアクセスを具体的には付与されません、 **LocalService**アカウント、ドライバーはできませんを使用します。 同様に、ミニドライバーは、名前付きイベント オブジェクトを作成する場合、同じアクセスまたはアプリケーション イベント オブジェクトを使用することができなく付与する必要があります。

-   アウト プロセス COM オブジェクト

    そのコンポーネントは、適切なアクセス許可を明示的に付与しない限り、作成するか、アウト プロセス COM インターフェイスを使用するあらゆる試みは失敗を**LocalService**アカウント。 たとえば、呼び出し**CoCreateInstance**または**CoCreateInstanceEx** (両方が、Microsoft Windows SDK ドキュメントで説明)、CLSCTX で\_ローカル\_サーバー フラグセットは、コンポーネントにアクセス許可を付与しない場合に失敗することが、 **LocalService**アカウント。 同様に、ドライバーをドライバーにプロセス内ではない COM インターフェイスへのポインターを使用しようとして失敗します。 これは、コンポーネントが、ドライバーを呼び出し、されるドライバーできるコールバック インターフェイスにインターフェイスへのポインターを渡す場合に発生します。

-   作成してプロセスを開く

    WIA ドライバーが他のプロセスを手動で開始しない必要があります (呼び出すことによって、たとえば、 **CreateProcess**または**CreateProcessAsUser**)。 この動作は ドライバーの成功が**LocalSystem**アカウント、不要になった可能性がそのためには、新しいドライバー **LocalService**アカウント。 詳細については**CreateProcess**と**CreateProcessAsUser**、Windows SDK のマニュアルを参照してください。

 

 




