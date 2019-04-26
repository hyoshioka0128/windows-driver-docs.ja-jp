---
title: 付録 4 ドライバー署名の問題
description: 2 つの既知のドライバーの署名に関する問題を以下に示します。
ms.assetid: EC244022-A02B-4AAD-93EE-B9AE3E72A674
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1592fab6e387c7d4c01c005e62dcdaad77403b96
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342012"
---
# <a name="appendix-4-driver-signing-issues"></a>付録 4:ドライバーの署名の問題


2 つの既知のドライバーの署名に関する問題を以下に示します。

## <a name="signing-issue-with-previous-os"></a>以前の OS に署名に関する問題


新しい証明書を新規または既存のベンダーはすべての新しいリリースの Windows およびその後にリリースされたこのサービス パック、認定済み CA ベンダーは Microsoft からルート証明書、OS イメージに追加されます。 たとえば、Vista、XP などです。Os があります。 テスト対象のコンピューターがインターネットに接続されていない場合、不明な問題やドライバーを署名しない署名の問題。 テスト対象コンピューターをインターネットに接続し、新しい証明書はドライバーをインストールすると、問題があれば表示されない、ダウンロードに自動的にされます。 場合によって CA ベンダーでは、テスト対象のコンピューターがインターネットに接続されていない場合、問題の解決に役に立つことができます。

## <a name="code-52-error"></a>52 コード エラー


既知のバグがあるため、Windows 7 x64 OS では、カタログ ファイル (.cat) ときに新しい VeriSign にリリースされた署名証明書を使って、SHA256 を使用する署名アルゴリズムでは、します。 符号付き cat ファイルとビューの署名を開き、[詳細] タブを選択すると、次が表示されます。

![署名のハッシュ アルゴリズムを示すスクリーン ショット](images/tutorialcertsignaturehashalg.png)

問題を解決するには、VeriSign、SHA1 ハッシュ アルゴリズムで署名されたコストなしでの証明書を置き換えるを提供するを確認することがあります。

または、別の SHA1 証明書を購入し、次に示す両方の証明書を保持するかどうかは 2 つのシグネチャを持つファイルに署名します。 .Sys ファイルのみできるデュアル PE ファイルであるために、署名に注意してください。

```cpp
Signtool sign /fd sha256 /ac C:\MyCrossCert\Crosscert.cer /s my /n “MyCompany Inc. “ /ph /as /sha1 XX...XX C:\DriverDir\toaster.SYS
```

場所 XX.XX は、セカンダリ署名を使用する証明書のハッシュです。 タイムスタンプの署名に/tr を追加します。

**注**  マイクロソフト セキュリティ アドバイザリを確認してください ([2880823](https://technet.microsoft.com/library/security/2880823))"非推奨の sha-1 ハッシュ アルゴリズムの Microsoft Root Certificate Program"を記述するポリシーの変更、Microsoft がありません現在の SSL とコード署名の 2016 年 1 月 1 日の後の目的の sha-1 ハッシュ アルゴリズムを使用して X.509 証明書を発行する証明書機関のルートを許可します。

 

SHA1 証明書の使用は、Microsoft は 2016 年 1 月 1日から始まるで廃止される予定です。 すべての CA ベンダーは、SHA256 ハッシュ アルゴリズムによる証明書の署名を発行する必要があります。

Windows では、SHA1 コードが 2016 年 1 月 1 日の後のタイムスタンプなしの証明書の署名の受け入れを停止します。

 

 





