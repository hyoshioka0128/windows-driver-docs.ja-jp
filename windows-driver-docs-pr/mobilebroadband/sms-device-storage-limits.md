---
title: SMS デバイス ストレージの制限
description: SMS デバイス ストレージの制限
ms.assetid: b2491562-352e-4881-99c7-98d43aeec64b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976c7b48b996848c3cdfa9bac7292e56724dbe1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323664"
---
# <a name="sms-device-storage-limits"></a>SMS デバイス ストレージの制限


SMS クライアント アプリでは、メッセージ キューとして SMS デバイス ストレージを使用する必要があります。 デバイスで SMS ストレージの合計は異なりますが、デバイスの記憶域は通常、30 メッセージに制限されます。

モバイル ブロード バンド SMS プラットフォームは、ユーザー データの削除を最小限に抑えながら、SMS デバイスの記憶域スペースを解放することで新しい受信 SMS メッセージを受信する機能を維持するために設計されています。

デバイスは、SMS の記憶域がいっぱいになった場合、新しい SMS メッセージを受信できません。 Windows は、重要なモバイル ネットワーク オペレーターの通知などの新しい受信 SMS データを受信する権限を確認するデバイスの記憶域から古い SMS メッセージを自動的に削除します。

次はお勧めします。

-   SMS クライアント アプリは、SMS の記憶域デバイスではなくメッセージの履歴を維持するためにローカル アプリの記憶域を使用する必要があります。

-   SMS クライアント アプリでは、読み取り時にメッセージを削除しないでください。 SMS クライアント アプリは、Windows デバイスの記憶域がいっぱいになったときに、古いメッセージを自動的に削除できるようにする必要があります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SMS のアプリの開発](developing-sms-apps.md)

 

 






