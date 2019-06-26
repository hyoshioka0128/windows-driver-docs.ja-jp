---
title: テスト オートメーション ツール
description: GPIO テスト自動化はミット プラットフォームを使用します。
ms.assetid: F6C4FCC2-210B-4B6E-9D1A-77842E470025
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1feb2891fd4820e0396b61b013253f0855bc4bb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373558"
---
# <a name="test-automation-tools"></a>テスト オートメーション ツール


GPIO テスト自動化はミット プラットフォームを使用します。

最初に、次を参照してください。[ミットで GPIO テスト](https://docs.microsoft.com/windows-hardware/drivers/spb/gpio-tests-in-mitt)します。 インストーラーをダウンロード、コンテンツを展開し、読み取り、 **ReadMe**ファイル ツールの概要。

ツールをテスト対象のシステムに接続するには、GPIO ボタンとインジケーター pin アウトが必要です。 ボードを設定して、その関連するパッケージがインストールされている後、は、次の方法のいずれかで使用できます。

-   GPIO ボタンおよびインジケーターのシナリオの両方の既存のオートメーション テストを実行します。
-   追加のシナリオの詳細については、パターン ジェネレーターを使用します。

テスト バイナリ ミット ツール インストーラーの一部であります。 テストを開始するには、ミット ドキュメントのセクションの「実行中の GPIO automation」」の手順に従います。

ミット ツールは、さまざまなボタンを押す操作 (保留中 ボタンを押して下キーを押しますおよびボタンを放す) の等価をシミュレートするために必要な GPIO インパルスを直接生成できます。 テストが[SimpleIo](https://go.microsoft.com/fwlink/p/?linkid=296486)に基づいており、電源の遷移を同期受信インジケーターなどの問題を検出できます。

**注**  ミット プラットフォームがカスタマイズされた入力パターンに対応できる簡単にします。 これらを生成する方法の手順については、ミット Readme ファイルを参照してください。

 

 

 




