---
title: MobileBroadbandAccount オブジェクトを作成する
description: MobileBroadbandAccount オブジェクトを作成する
ms.assetid: 631e885f-67bb-4c30-a82f-352c23cc973a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b190478e57d2789d49fa8aa9a8f143863531e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377635"
---
# <a name="create-a-mobilebroadbandaccount-object"></a>MobileBroadbandAccount オブジェクトを作成する


[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)オブジェクトは、ネットワーク アカウントを表す、このようなオブジェクトを作成するネットワーク アカウントの ID が必要です。 モバイル ブロード バンド アプリがネットワークの一覧から開始されると、タイルの起動コントラクトへのパラメーターとして使用するネットワーク アカウント ID を受け取ります。

タイルから直接、アプリがアクティブの場合、タイルの起動コントラクトに関連付けられているパラメーターがないの値を取得する必要があります、 [ **AvailableNetworkAccountIds** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_AvailableNetworkAccountIds)の静的プロパティ、[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)クラス。 各文字列の 1 つのアカウント ID を文字列の読み取り専用コレクションが返されます このメソッドが 1 つの文字列を含むコレクションを返す場合は、以降のすべてのアクションを実行する必要はありません。 次の JavaScript コードの例では、これを行う方法を示します。

``` syntax
var myNetworkAccountId;
var allNetworkAccountIds = Windows.Networking.NetworkOperators.MobileBroadbandAccount.availableNetworkAccountIds;

if (allNetworkAccountIds.size == 1)
{
  myNetworkAccountId = allNetworkAccountIds[0]; 
}
```

返されるコレクションに 1 つ以上の文字列が含まれている場合は、アプリケーションを実行しているエンド ユーザーからの入力を必要があります。 コレクションを反復処理する方法の 1 つは、作成、 [ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)各アカウントの ID、コレクション内のオブジェクトし、オブジェクト (たとえば、電話番号) のプロパティを使用してリスト ボックス コントロールを設定します。 ユーザーが選択した後と、エンドユーザーにこのコントロールが表示される他のすべての**MobileBroadbandAccount**オブジェクトを解放できます。

アカウント ID がある場合は後の呼び出し、 [ **CreateFromNetworkAccountId** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CreateFromNetworkAccountId_System_String_)クラスの静的メソッド[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)します。 次のコード例では、JavaScript を使用してこれを行う方法を示します。

``` syntax
var myNetworkAccountId = "{95499FEF-1579-4547-A0BE-FF271ADBBE76}";
var myNetworkAccountObject = Windows.Networking.NetworkOperators.MobileBroadbandAccount.createFromNetworkAccountId(myNetworkAccountId);
```

## <a name="span-idemptylistspanspan-idemptylistspanmobilebroadbandaccountavailablenetworkaccountids-returns-an-empty-list"></a><span id="emptylist"></span><span id="EMPTYLIST"></span>MobileBroadbandAccount.AvailableNetworkAccountIds が空のリストを返します


アプリが信頼されていない場合は、ユーザーのコンピューターに 1 つ以上のネットワーク オペレーターからアカウントがあるために、例外をスローする代わりに空のコレクションを返します。 [ **AvailableNetworkAccountIds** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_AvailableNetworkAccountIds)プロパティは、アプリのメタデータ パッケージの参照が許可されているアカウント Id のみを返します。 **AvailableNetworkAccountIds**プロパティが各アカウント ID が取得時に関連付けられているデバイスを持つことを確認しますこのプロパティがあっても、空のコレクションを返すことができます、 [  **。CreateFromNetworkAccountId** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CreateFromNetworkAccountId_System_String_)アクセス拒否例外はスローされません。

これは、ネットワーク ハードウェアが検出されない場合、またはネットワーク ハードウェアが、アクセス可能な SIM を持っていない場合に発生することができます。 なぜ、返されたコレクションが空の正確な理由を特定する簡単な方法では、WWAN ログを確認します。 検索テキストが含まれるエントリは、テキスト ログ ファイルのログを収集したら**AvailableNetworkAccountIds**します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 






